<script lang="ts">
	import { onMount } from 'svelte';

	let hiddenElements;

	let observer: any;

	onMount(() => {
		observer = new window.IntersectionObserver((entries) => {
			entries.forEach((entry) => {
				if (entry.isIntersecting) {
					entry.target.classList.add('show');
				}
			});
		});

		hiddenElements = document.querySelectorAll('.hidden');
		hiddenElements.forEach((el) => observer.observe(el));
		//Show content

		// Setting display to block :
		const contents = document.querySelectorAll('.content') as NodeListOf<HTMLDivElement>;
		function showContents() {
			// Affiche tous les éléments avec la classe ".content"
			const loader = document.querySelector('.loader') as HTMLDivElement;
			if (loader) {
				if (loader.style.display === 'none') {
					contents.forEach((content) => {
						content.style.display = 'block';
					});
				}
			}
		}
		showContents();
	});
</script>

<contact class="content">
	<section id="section-1">
		<a href="/" class="hidden">Who are we ?</a>
		<p class="hidden firstp">
			The question of human identity has been debated for millennia by philosophers, thinkers, and
			scientists. It touches both on our intrinsic nature and our place in the universe. The
			complexity of this question lies in the fact that our identity is multi-dimensional and
			evolving.
		</p>
	</section>
	<section id="section-2">
		<h1 class="hidden">Who am i ?</h1>
		<p class="hidden secondp">
			The quest for our identity is an exciting and never-ending journey, as we continue to grow,
			evolve, and redefine ourselves throughout our lives. It is through this self-exploration that
			we can find a deeper meaning to our existence and a connection with the world around us.
		</p>
	</section>
	<section id="section-3">
		<p class="hidden">
			My name is Enzo, im a freelance web developper<br />I love to create immersive experiences<br
			/>Take the time to enjoy this moment, breath and relax
		</p>
	</section>
</contact>

<style lang="scss">
	contact {
		position: absolute;
		background: #000;
		height: 100vh;
		width: 100%;
		color: white;
		animation: fadeIn 1s ease forwards;
		overflow-y: scroll;
		scroll-snap-type: y mandatory;
		section {
			display: flex;
			justify-content: center;
			align-items: center;
			flex-direction: column;
			text-align: center;
			width: 100%;
			height: 200vh;
			scroll-snap-align: center;
		}
		#section-1 {
			height: 100vh;
			background: rgb(65, 63, 63);
		}
		#section-2 {
			background: rgb(84, 80, 80);
		}
		.firstp {
			transition-delay: 400ms;
			max-width: 400px;
		}
		.secondp {
			transition-delay: 400ms;
			max-width: 400px;
		}
		h1 {
			font-size: 5em;
		}
		a {
			text-decoration: none;
			color: white;
			font-size: 3em;
		}
		p {
			text-align: center;
		}
	}
	@keyframes fadeIn {
		0% {
			transform: translateY(100%);
			filter: blur(5px);
		}
		100% {
			transform: translateY(0%);
			filter: blur(0px);
		}
	}
</style>
