<script lang="ts">
	import { onMount } from 'svelte';
	import '../style/style.scss';
	let audio:HTMLAudioElement
	onMount(() => {
		window.addEventListener("click", () => {
			audio.play()
		})
	})
</script>

<svelte:head>
	<title>Reelax - Immersive Xperience</title>
	<link rel="shortcut-icon" href="/sleeping.png" />
	<link rel="icon" href="/sleeping.png" />
	<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" integrity="sha512-iecdLmaskl7CVkqkXNQ/ZH/XLlvWZOJyj7Yy7tcenmpD1ypASozpmT/E0iPtmFIB46ZmdtAc9eNBvH0H/ZpiBw==" crossorigin="anonymous" referrerpolicy="no-referrer" />
</svelte:head>
<audio bind:this={audio} loop>
	<source src="/music.mp3" type="audio/mpeg" />
</audio>
<slot />
