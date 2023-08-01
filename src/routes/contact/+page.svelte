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
	});
</script>

<contact class="content">
	<section class="1">
		<a href="/" class="hidden">Who are we ?</a>
		<p class="hidden firstp">
			The question of human identity has been debated for millennia by philosophers, thinkers, and
			scientists. It touches both on our intrinsic nature and our place in the universe. The
			complexity of this question lies in the fact that our identity is multi-dimensional and
			evolving.
		</p>
	</section>
	<section>
		<h1 class="hidden">Who am i ?</h1>
		<p class="hidden secondp">
			The quest for our identity is an exciting and never-ending journey, as we continue to grow,
			evolve, and redefine ourselves throughout our lives. It is through this self-exploration that
			we can find a deeper meaning to our existence and a connection with the world around us.
		</p>
	</section>
	<section class="hidden">
		<p>
			My name is Enzo, im a freelance web developper<br />I love to create immersive experiences<br
			/>Take the time to enjoy this moment, breath and relax
		</p>
	</section>
</contact>

<style lang="scss">
	contact {
		position: absolute;
		background: #000;
		width: 100%;
		min-height: 250vh;
		color: white;
		animation: fadeIn 1s ease forwards;
		display: flex;
		padding: 300px 0;
		justify-content: space-between;
		gap: 60px;
		align-items: center;
		flex-direction: column;
		overflow: hidden;
		section {
			text-align: center;
			max-width: 400px;
		}
		.firstp {
			transition-delay: 400ms;
		}
		.secondp {
			transition-delay: 400ms;
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
