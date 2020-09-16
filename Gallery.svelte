<script>
    export let gap = 10;
    export let maxColumnWidth = 250;

    let slotHolder = null;
    let columns = [];
    let galleryWidth = 0;
    let columnCount = 0;
    
    $: columnCount = parseInt(galleryWidth / maxColumnWidth);
    $: galleryStyle = `grid-template-columns: repeat(${columnCount}, 1fr); --gap: ${gap}px`;

    function Draw() {
        const images = Array.from(slotHolder.childNodes).filter(child => child.tagName === "IMG");

        // Generate an array of empty arrays ([[] * columnCount])
        columns = [...Array(columnCount).keys()].map(() => []);

        // Fill the columns with image URLs
        for (let i=0; i<images.length; i++) {
            columns[i % columnCount].push(images[i].src);
        }
    }
</script>

<div id="slotHolder" bind:this={slotHolder} on:DOMNodeInserted={ Draw }>
    <slot></slot>
</div>

{#if columns}
<div id="gallery" bind:clientWidth={galleryWidth} style={galleryStyle}>
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
    #slotHolder { display: none }
    #gallery { width: 100%; display: grid; gap: var(--gap) }
    #gallery .column { display: flex; flex-direction: column }
    #gallery .column * {
        width: 100%;
        margin-top: var(--gap);
        transition: transform .3s;
        border: 1px solid white;
    }
    #gallery .column *:nth-child(1) { margin-top: 0 }
</style>