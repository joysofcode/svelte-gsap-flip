<div class="container">
	<ul>
		<li>
			<a href="/01-flip">1. FLIP</a>
		</li>
		<li>
			<a href="/02-circles">2. Circles</a>
		</li>
		<li>
			<a href="/03-grid">3. Grid</a>
		</li>
		<li>
			<a href="/04-movies">4. Movies</a>
		</li>
	</ul>
</div>

<style>
	.container {
		height: calc(100vh - 4rem);
		display: grid;
		place-content: center;
	}

	ul {
		margin: 0;
		padding: 0;
		list-style: none;
		font-size: 4vw;
	}

	li {
		padding: 2rem;
	}

	li:not(:last-child) {
		border-bottom: 1px solid hsl(220 10% 40%);
	}

	a {
		color: inherit;
		text-decoration: none;
	}
</style>
