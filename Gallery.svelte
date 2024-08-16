<script>
// @ts-nocheck

    import { onMount, onDestroy, createEventDispatcher } from "svelte";
    import { tick } from "svelte";

	/**
	 * @type {number}
	 */
    export let gap = 10;

	/**
	 * @type {number}
	 */
    export let maxColumnWidth = 250;

	/**
	 * @type {boolean}
	 */
    export let hover = false;

	/**
	 * @type {'eager' | 'lazy'}
	 */
    export let loading = 'lazy';

    const dispatch = createEventDispatcher();

	/**
	 * @type {HTMLElement | null}
	 */
    let slotHolder = null;

	/**
	 * @type {HTMLImageElement[]}
	 */
    let columns = [];

	/**
	 * @type {number}
	 */
    let galleryWidth = 0;

	/**
	 * @type {number}
	 */
    let columnCount = 0;

    // @ts-ignore
    $: columnCount = parseInt(galleryWidth / maxColumnWidth) || 1;
    $: columnCount && Draw();
    $: galleryStyle = `grid-template-columns: repeat(${columnCount}, 1fr); --gap: ${gap}px`;

    onMount(Draw);
	onDestroy(Draw)

	
	// @ts-ignore
    function HandleClick(e) {
        dispatch("click", { src: e.target.src, alt: e.target.alt, loading: e.target.loading, class: e.target.className });
    }

    async function Draw() {
        await tick();

        if (!slotHolder) {
            return;
        }

        const images = Array.from(slotHolder.childNodes).filter(
            // @ts-ignore
            (child) => child.tagName === "IMG"
        );

		/**
		 * @type {HTMLImageElement[]}
		 */
        columns = [];

        // Fill the columns with image URLs
        for (let i = 0; i < images.length; i++) {
            const idx = i % columnCount;
			// @ts-ignore
            columns[idx] = [
				// @ts-ignore
                ...(columns[idx] || []),
				// @ts-ignore
                { src: images[i].src, alt: images[i].alt, class: images[i].className },
            ];
        }
    }
</script>

<div
    id="slotHolder"
    bind:this={slotHolder}
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
						on:keydown={HandleClick}
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
