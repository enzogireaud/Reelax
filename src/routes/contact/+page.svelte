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

<contact>
	<section>
		<a href="/">Who am i ?</a>
	</section>
	<section class="hidden">
		<h1>Who am i ?</h1>
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
		min-height: 300vh;
		color: white;
		animation: fadeIn 1s ease forwards;
		display: flex;
		padding: 300px 0;
		justify-content: space-between;
		gap: 60px;
		align-items: center;
		flex-direction: column;
		overflow: hidden;
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
