<script lang="ts">
	import '../style/style.scss';
</script>

<svelte:head>
	<title>Reelax - Immersive Xperience</title>
	<link rel="shortcut-icon" href="/sleeping.png" />
	<link rel="icon" href="/sleeping.png" />
</svelte:head>
<audio autoplay loop={true}>
	<source src="/music.mp3" type="audio/mpeg" />
</audio>
<slot />
