# svelte-image-gallery

Fluid Image Container for Svelte

| Traditional | svelte-image-gallery |
| ----------- | -------------------- |
| ![traditional][ss1] | ![svelte-image-gallery][ss2] |
| Made responsive via media queries or [minmax/autofit][minmax] | Responsive out of the box |

[ss1]: https://i.imgur.com/rTSftEw.jpg
[ss2]: https://i.imgur.com/CpgVaWm.jpg
[minmax]: https://css-tricks.com/intrinsically-responsive-css-grid-with-minmax-and-min/

### Installation

run `npm i svelte-image-gallery --save-dev`

### Usage

``` svelte
<script>
	import Gallery from 'svelte-image-gallery'
</script>

<Gallery>
	<img src="..." />
	<img src="..." />
	...
</Gallery>
```

### Parameters

| Parameter  | Default | Description                 |
| gap        | 10      | Grid Gap Between Items (px) |
| breakpoint | 250     | Maximum Image Width         |

> Created By [Berkin AKKAYA](https://berkinakkaya.github.io)