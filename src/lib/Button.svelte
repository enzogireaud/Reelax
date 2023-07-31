<button><a href="/contact">Start</a></button>

<style lang="scss">
	button {
		position: absolute;
		left: 50%;
		top: 50%;
		width: 218px;
		height: 75px;
		transform: translateX(-50%);
		border-radius: 80px;
		background: none;
		border: none;
		cursor: pointer;
		text-transform: uppercase;
		transition: 1s ease;
		font-family: 'Cormorant Garamond', serif;
		font-size: 2em;
		&:hover {
			letter-spacing: 15px;
			transform: translateX(-50%) scale(1.2);
		}
		a {
			text-decoration: none;
			color: whitesmoke;
		}
	}
</style>
