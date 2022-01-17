<script>
	import Gallery from "svelte-image-gallery";

	function HandleClick(e) {
		console.log(e.detail.src)
	}
</script>

<Gallery gap={15} maxColumnWidth={250} on:click={HandleClick}>
	<img src="https://via.placeholder.com/210x170/100" alt="210x170 Res" />
	<img src="https://via.placeholder.com/180x200/100" alt="180x200 Res" />
	<img src="https://via.placeholder.com/200x210/100" alt="200x210 Res" />
	<img src="https://via.placeholder.com/140x250/100" alt="140x250 Res" />
	<img src="https://via.placeholder.com/250x300/100" alt="250x300 Res" />
	<img src="https://via.placeholder.com/280x200/100" alt="280x200 Res" />
	<img src="https://via.placeholder.com/220x180/100" alt="220x180 Res" />
	<img src="https://via.placeholder.com/180x150/100" alt="180x150 Res" />
	<img src="https://via.placeholder.com/210x210/100" alt="210x210 Res" />
	<img src="https://via.placeholder.com/200x200/100" alt="200x200 Res" />
	<img src="https://via.placeholder.com/220x200/100" alt="220x200 Res" />
	<img src="https://via.placeholder.com/180x310/100" alt="180x310 Res" />
	<img src="https://via.placeholder.com/210x210/100" alt="210x210 Res" />
	<img src="https://via.placeholder.com/200x280/100" alt="200x280 Res" />
	<img src="https://via.placeholder.com/210x350/100" alt="210x350 Res" />
	<img src="https://via.placeholder.com/180x270/100" alt="180x270 Res" />
</Gallery>
