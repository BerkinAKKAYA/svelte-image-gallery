<script>
    import { onMount } from "svelte";

    export let gap = 10;
    export let breakpoint = 250;

    let clientWidth = 0;
    let urls = [];
    let columnCount = 0;
    let columns = [];
    let gallery = null;
    let slotHeight = 0;
    let main = null;
    let childCount = 0;

    onMount(async () => {
        main = document.querySelector("#slotHolder");
    });

    $: columnCount = parseInt(clientWidth / breakpoint);
    $: if (slotHeight) { childCount = main ? main.childNodes.length : 0 };
    $: {
        if (columnCount && urls && childCount) {
            Redraw();
        }
    }

    function Redraw() {
        urls = main ? Array.from(main.childNodes).filter(a => a.src).map(a => a.src) : [];
        columns = [];

        for (let i=0; i<columnCount; i++) {
            columns[i] = [urls[i]];
        }

        Draw(columnCount);
    }

    async function Draw(i) {
        if (isNaN(i) || i >= urls.length) { return }

        const col = SmallestColumn();
        columns[col] = [...columns[col] || [], urls[i]];

        await new Promise((resolve, reject) => setTimeout(resolve, 0))
        Draw(i + 1);
    }

    function SmallestColumn() {
        const HeightOf = column => {
            let height = 0;
            column.childNodes.forEach(el => { height += el.height || 0 });
            return height;
        }

        const columns = gallery.querySelectorAll(".column");
        let min = 0;

        for (let i=0; i<columns.length; i++) {
            if (HeightOf(columns[i]) < HeightOf(columns[min])) {
                min = i;
            }
        }

        return min;
    }
</script>

<div id="slotHolder" bind:clientHeight={slotHeight}><slot></slot></div>

{#if columns}
    <div id="gallery" bind:this={gallery} bind:clientWidth style="grid-template-columns: repeat({columnCount}, 1fr); --gap: {gap}px">
        {#each columns as column}
            <div class="column">
                {#each column as url}
                    <img src={url} alt="" />
                {/each}
            </div>
        {/each}
    </div>
{/if}

<style>
    #gallery { width: 100%; display: grid; gap: var(--gap) }
    #gallery .column { display: flex; flex-direction: column }
    #gallery .column * {
        width: 100%;
        margin-top: var(--gap);
        transition: transform .3s;
        border: 1px solid white;
    }
    #gallery .column *:nth-child(1) { margin-top: 0 }
    #slotHolder {
        display: grid;
        grid-template-columns: 1fr;
        position: absolute;
        visibility: hidden;
    }
</style>