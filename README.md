# svelte-image-gallery

[![MadeWithSvelte.com shield](https://madewithsvelte.com/storage/repo-shields/2648-shield.svg)](https://madewithsvelte.com/p/svelte-image-gallery/shield-link)

A Masonry-Like Image Container for Svelte

[See On REPL][repl]

| Traditional                                                   | svelte-image-gallery         |
| ------------------------------------------------------------- | ---------------------------- |
| ![traditional][ss1]                                           | ![svelte-image-gallery][ss2] |
| Made responsive via media queries or [minmax/autofit][minmax] | Responsive out of the box    |

[ss1]: https://i.imgur.com/rTSftEw.jpg
[ss2]: https://i.imgur.com/CpgVaWm.jpg
[minmax]: https://css-tricks.com/intrinsically-responsive-css-grid-with-minmax-and-min
[repl]: https://svelte.dev/repl/29b37509123b4a4bac808531f39d7d9e?version=3.24.1

### Installation

```sh
npm install --save-dev svelte-image-gallery
```

### Usage

```svelte
<script>
	import Gallery from 'svelte-image-gallery'

	function handleClick(e) {
		console.log(e.detail.url)
	}
</script>

<Gallery on:click={handleClick}>
	<img src="..." />
	<img src="..." />
	...
</Gallery>
```

### Running Locally

-   Clone the repository
-   Open `example` folder in terminal
-   Run `npm i`, then `npm run dev`

### Parameters

| Parameter      | Default | Description            | Unit |
| -------------- | ------- | ---------------------- | ---- |
| gap            | 10      | Grid Gap Between Items | px   |
| maxColumnWidth | 250     | Maximum Column Width   | px   |
| hover          | false   | Enlarge Image on Hover | bool |
| loading        | eager   | Image Loading Type     | [mdn](https://developer.mozilla.org/en-US/docs/Web/API/HTMLImageElement/loading) |

To access the image url on click, use the `on:click` directive in the Gallery component.


> Created By [Berkin AKKAYA](https://berkinakkaya.github.io)
