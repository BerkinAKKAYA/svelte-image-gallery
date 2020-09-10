# svelte-image-gallery

Fluid Image Container for Svelte

[See On REPL][repl]

| Traditional | svelte-image-gallery |
| ----------- | -------------------- |
| ![traditional][ss1] | ![svelte-image-gallery][ss2] |
| Made responsive via media queries or [minmax/autofit][minmax] | Responsive out of the box |

[ss1]: https://i.imgur.com/rTSftEw.jpg
[ss2]: https://i.imgur.com/CpgVaWm.jpg
[minmax]: https://css-tricks.com/intrinsically-responsive-css-grid-with-minmax-and-min
[repl]: https://svelte.dev/repl/29b37509123b4a4bac808531f39d7d9e?version=3.24.1

### Installation
```sh
npm i svelte-image-gallery --save-dev
```

### Usage

```svelte
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
| ---------  | ------- | -----------                 |
| gap        | 10      | Grid Gap Between Items (px) |
| breakpoint | 250     | Maximum Image Width         |

> Created By [Berkin AKKAYA](https://berkinakkaya.github.io)
