<script lang="ts">
	import { onMount } from 'svelte';
	import '../style/style.scss';
	let audio: HTMLAudioElement;
	onMount(() => {
		window.addEventListener('click', () => {
			audio.play();
		});
		load();
	});

	function load() {
		// La page HTML est chargée, commencez le chargement des autres ressources ici
		let progress = 0;

		const contents = document.querySelectorAll('.content') as NodeListOf<HTMLDivElement>;

		function showContents() {
			// Affiche tous les éléments avec la classe ".content"
			contents.forEach((content) => {
				content.style.display = 'block';
			});
		}

		function incrementLoader() {
			// Incrémentez la valeur de "progress" jusqu'à atteindre 100
			if (progress < 100) {
				progress += 1; // Augmentez la valeur pour contrôler la vitesse du loader
				setTimeout(incrementLoader, 30); // Délai avant d'augmenter la valeur suivante (plus petit pour une meilleure animation)
			} else {
				// Une fois le chargement terminé, affichez tous les éléments avec la classe ".content"
				showContents();

				// Masquez le loader
				const loader = document.querySelector('.loader') as HTMLDivElement;
				if (loader) {
					loader.style.display = 'none';
				}
			}
		}

		incrementLoader();
	}
</script>

<svelte:head>
	<title>Reelax - Immersive Xperience</title>
	<link rel="shortcut-icon" href="/sleeping.png" />
	<link rel="icon" href="/sleeping.png" />
	<link
		rel="stylesheet"
		href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css"
		integrity="sha512-iecdLmaskl7CVkqkXNQ/ZH/XLlvWZOJyj7Yy7tcenmpD1ypASozpmT/E0iPtmFIB46ZmdtAc9eNBvH0H/ZpiBw=="
		crossorigin="anonymous"
		referrerpolicy="no-referrer"
	/>
</svelte:head>
<audio bind:this={audio} loop>
	<source src="/music.mp3" type="audio/mpeg" />
</audio>
<div class="loader wrapper">
	<div class="loader loader1">
		<div>
			<div>
				<div>
					<div>
						<div>
							<div />
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
	<img src="/click.webp" alt="Click" />
</div>
<slot />

<style lang="scss">
	.loader {
		position: absolute;
		background: #000;
		width: 100%;
		height: 100vh;
		z-index: 1000;
		color: white;
		justify-content: center;
		align-items: center;
		font-size: 2em;
		display: flex;
		gap: 20px;
		img {
			margin-top: 200px;
			z-index: 10000;
			animation: animate 3s linear forwards;
		}
	}
	@keyframes animate {
		0% {
			opacity: 0;
		}
		50% {
			opacity: 1;
		}
		100% {
			opacity: 0;
		}
	}
</style>
