<script>
	import Gallery from "../Gallery.svelte";

	function HandleClick(e) {
		console.log(
			`src: ${e.detail.src}, alt: ${e.detail.alt}, loading: ${e.detail.loading}, class: ${e.detail.class}`
		);
	}
</script>

<Gallery
	gap={15}
	maxColumnWidth={250}
	on:click={HandleClick}
	hover={true}
	loading="lazy"
>
	<img
		src="https://via.placeholder.com/210x170/100"
		alt="210x170"
		class="Hi"
	/>
	<img src="https://via.placeholder.com/180x200/100" alt="180x200" />
	<img src="https://via.placeholder.com/200x210/100" alt="200x210" />
	<img src="https://via.placeholder.com/140x250/100" alt="140x250" />
	<img src="https://via.placeholder.com/250x300/100" alt="250x300" />
	<img src="https://via.placeholder.com/280x200/100" alt="280x200" />
	<img src="https://via.placeholder.com/220x180/100" alt="220x180" />
	<img src="https://via.placeholder.com/180x150/100" alt="180x150" />
	<img src="https://via.placeholder.com/210x210/100" alt="210x210" />
	<img src="https://via.placeholder.com/200x200/100" alt="200x200" />
	<img src="https://via.placeholder.com/220x200/100" alt="220x200" />
	<img src="https://via.placeholder.com/180x310/100" alt="180x310" />
	<img src="https://via.placeholder.com/210x210/100" alt="210x210" />
	<img src="https://via.placeholder.com/200x280/100" alt="200x280" />
	<img src="https://via.placeholder.com/210x350/100" alt="210x350" />
	<img src="https://via.placeholder.com/180x270/100" alt="180x270" />
</Gallery>
