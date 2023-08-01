<script lang="ts">
	import Button from '$lib/Button.svelte';
	import { onMount } from 'svelte';

	let canvas: HTMLCanvasElement;

	onMount(async () => {
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

		// Initialization
		canvas.width = window.innerWidth;
		canvas.height = window.innerHeight;
		let c = canvas.getContext('2d');
		let mouse: {
			x: number;
			y: number;
		} = {
			x: 0, // ou toute autre valeur de type 'number'
			y: 0 // ou toute autre valeur de type 'number'
		};
		let maxRadius: number = 25;

		let colorArray = ['#ced4da', '#adb5bd', '#6c757d', '#495057', '#343a40'];

		window.addEventListener('mousemove', (event) => {
			mouse.x = event.x;
			mouse.y = event.y;
		});

		window.addEventListener('resize', () => {
			canvas.width = window.innerWidth;
			canvas.height = window.innerHeight;
			init();
		});

		class Circle {
			x: number;
			y: number;
			dx: number;
			dy: number;
			radius: number;
			minRadius: number;
			color: string;

			constructor(x: number, y: number, dx: number, dy: number, radius: number) {
				this.x = x;
				this.y = y;
				this.dx = dx;
				this.dy = dy;
				this.radius = radius;
				this.minRadius = radius;
				this.color = colorArray[Math.floor(Math.random() * colorArray.length)];
			}
			draw() {
				c?.beginPath();
				c?.arc(this.x, this.y, this.radius, 0, Math.PI * 2, false);
				if (c) {
					c.fillStyle = this.color;
				}
				c?.fill();
			}
			update() {
				if (this.x + this.radius > innerWidth || this.x - this.radius < 0) {
					this.dx = -this.dx;
				}
				if (this.y + this.radius > innerHeight || this.y - this.radius < 0) {
					this.dy = -this.dy;
				}
				this.y += this.dy;
				this.x += this.dx;

				// Interactivity
				if (
					mouse.x - this.x < 50 &&
					mouse.x - this.x > -50 &&
					mouse.y - this.y < 50 &&
					mouse.y - this.y > -50
				) {
					if (this.radius < maxRadius) {
						this.radius += 10;
					}
				} else if (this.radius > this.minRadius) {
					this.radius -= 1;
				}

				this.draw();
			}
		}
		let circleArray: any[] = [];

		function init() {
			circleArray = [];
			if (canvas.width < 900) {
				for (let i = 0; i < 50; i++) {
					let radius = Math.random() * 3 + 1;
					let x = Math.random() * (window.innerWidth - radius * 2) + radius;
					let y = Math.random() * (window.innerHeight - radius * 2) + radius;
					let dx = Math.random() - 0.5;
					let dy = Math.random() - 0.5;
					circleArray.push(new Circle(x, y, dx, dy, radius));
				}
			} else {
				for (let i = 0; i < 800; i++) {
					let radius = Math.random() * 3 + 1;
					let x = Math.random() * (window.innerWidth - radius * 2) + radius;
					let y = Math.random() * (window.innerHeight - radius * 2) + radius;
					let dx = Math.random() - 0.5;
					let dy = Math.random() - 0.5;
					circleArray.push(new Circle(x, y, dx, dy, radius));
				}
			}
		}

		function animate() {
			requestAnimationFrame(animate);
			c?.clearRect(0, 0, window.innerWidth, window.innerHeight);
			for (let i = 0; i < circleArray.length; i++) {
				circleArray[i].update();
			}
		}
		init();
		animate();
	});
</script>

<page class="content">
	<canvas bind:this={canvas} />
	<Button />
</page>

<style lang="scss">
	page {
		position: absolute;
		width: 100%;
		height: 100vh;
		overflow: hidden;
		cursor: none;
		canvas {
			animation: fadeIn 3s ease forwards;
		}
	}

	@keyframes fadeIn {
		0% {
			transform: scale(5);
			opacity: 0;
			filter: blur(5px);
		}
		100% {
			transform: scale(1);
			opacity: 1;
			filter: blur(0px);
		}
	}
	@keyframes fadeOut {
		0% {
			opacity: 0;
			filter: blur(0px);
		}
		50% {
			opacity: 1;
		}
		100% {
			opacity: 0;
		}
	}
</style>
