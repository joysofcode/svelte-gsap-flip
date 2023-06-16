<script lang="ts">
	export let data
</script>

<main class="movies">
	{#each data.movies as movie}
		<article>
			<a href="/04-movies/movie/{movie.id}">
				<div class="poster">
					<img
						class="cover"
						src={movie.poster_path}
						alt={movie.title}
						data-flip-id="cover-{movie.title}"
					/>
					<span class="score">{movie.vote_average}</span>
				</div>
			</a>

			<p class="title" data-flip-id="title-{movie.title}">
				{movie.title}
			</p>
		</article>
	{/each}
</main>

<style>
	.movies {
		display: grid;
		gap: 2rem;
		grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
	}

	.poster {
		position: relative;
		box-shadow: 1px 1px 10px hsl(0 0% 0% / 40%);
	}

	.cover {
		width: 100%;
		display: block;
		border-radius: 8px;
	}

	.score {
		display: flex;
		place-items: center;
		position: absolute;
		bottom: -24px;
		left: 10px;
		padding: 0.5rem;
		color: hsl(0 0% 98%);
		background-color: hsl(0 0% 0%);
		border: 2px solid hsl(0 0% 80%);
		border-radius: 50%;
		aspect-ratio: 1;
	}

	.title {
		margin-top: 3rem;
	}
</style>
