<script>
    import { onMount, createEventDispatcher } from "svelte";
    import { tick } from "svelte";

    export let gap = 10;
    export let maxColumnWidth = 250;
    export let hover = false;
    export let loading;

    const dispatch = createEventDispatcher();

    let slotHolder = null;
    let columns = [];
    let galleryWidth = 0;
    let columnCount = 0;

    $: columnCount = parseInt(galleryWidth / maxColumnWidth) || 1;
    $: columnCount && Draw();
    $: galleryStyle = `grid-template-columns: repeat(${columnCount}, 1fr); --gap: ${gap}px`;

    onMount(Draw);

    function HandleClick(e) {
        dispatch("click", { src: e.target.src, alt: e.target.alt, loading: e.target.loading, class: e.target.className });
    }

    async function Draw() {
        await tick();

        if (!slotHolder) {
            return;
        }

        const images = Array.from(slotHolder.childNodes).filter(
            (child) => child.tagName === "IMG"
        );
        columns = [];

        // Fill the columns with image URLs
        for (let i = 0; i < images.length; i++) {
            const idx = i % columnCount;
            columns[idx] = [
                ...(columns[idx] || []),
                { src: images[i].src, alt: images[i].alt, class: images[i].className },
            ];
        }
    }
</script>

<div
    id="slotHolder"
    bind:this={slotHolder}
    on:DOMNodeInserted={Draw}
    on:DOMNodeRemoved={Draw}
>
    <slot />
</div>

{#if columns}
    <div id="gallery" bind:clientWidth={galleryWidth} style={galleryStyle}>
        {#each columns as column}
            <div class="column">
                {#each column as img}
                    <img
                        src={img.src}
                        alt={img.alt}
                        on:click={HandleClick}
                        class="{hover === true ? "img-hover" : ""} {img.class}"
                        loading={loading}
                    />
                {/each}
            </div>
        {/each}
    </div>
{/if}

<style>
    #slotHolder {
        display: none;
    }
    #gallery {
        width: 100%;
        display: grid;
        gap: var(--gap);
    }
    #gallery .column {
        display: flex;
        flex-direction: column;
    }
    #gallery .column * {
        width: 100%;
        margin-top: var(--gap);
    }
    #gallery .column *:nth-child(1) {
        margin-top: 0;
    }
    .img-hover {
        opacity: 0.9;
        transition: all 0.2s;
    }
    .img-hover:hover {
        opacity: 1;
        transform: scale(1.05);
    }
</style>
