<script>
    import { onMount } from 'svelte';
    
    export let gap = 10;
    export let maxColumnWidth = 250;
    
    let slotHolder = null;
    let columns = [];
    let galleryWidth = 0;
    let columnCount = 0;
    
    $: columnCount = parseInt(galleryWidth / maxColumnWidth) || 1;
    $: columnCount && Draw();
    $: galleryStyle = `grid-template-columns: repeat(${columnCount}, 1fr); --gap: ${gap}px`;
    
    onMount(Draw);

    function Draw() {
        if (!slotHolder) { return }

        const images = Array.from(slotHolder.childNodes).filter(child => child.tagName === "IMG");
        columns = [];

        // Fill the columns with image URLs
        for (let i=0; i<images.length; i++) {
            const idx = i % columnCount;
            columns[idx] = [...columns[idx] || [], images[i].src];
        }
    }
</script>

<div id="slotHolder" bind:this={slotHolder} on:DOMNodeInserted={Draw} on:DOMNodeRemoved={Draw}>
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
    #gallery .column * { width: 100%; margin-top: var(--gap) }
    #gallery .column *:nth-child(1) { margin-top: 0 }
</style>
