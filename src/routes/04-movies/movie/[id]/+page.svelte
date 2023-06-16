<script lang="ts">
	import { page } from '$app/stores'

	export let data

	$: movie = data.movies.find((movie) => movie.id === $page.params.id)
</script>

{#if movie}
	<article>
		<div class="poster">
			<a href="/04-movies">
				<img
					class="cover"
					src={movie.poster_path}
					alt={movie.title}
					data-flip-id="cover-{movie.title}"
				/>
			</a>
		</div>

		<div class="details">
			<h1 class="title" data-flip-id="title-{movie.title}">
				{movie.title}
			</h1>
			<p class="overview">{movie.overview}</p>
		</div>
	</article>

	<div class="backdrop" style:--bg-image="url({movie.backdrop_path})" />
{/if}

<style>
	article {
		display: flex;
		gap: 2rem;
	}

	.poster {
		min-width: 300px;
		min-height: 450px;
	}

	.cover {
		width: 100%;
		height: 100%;
		aspect-ratio: 1;
		display: block;
		border-radius: 8px;
		box-shadow: 1px 1px 10px hsl(0 0% 0% / 40%);
	}

	.details {
		padding-block: 4rem;
	}

	.title {
		margin: 0;
	}

	.overview {
		max-width: 80ch;
	}

	.backdrop {
		position: fixed;
		inset: 0;
		background-image: var(--bg-image);
		background-size: cover;
		opacity: 0.04;
		z-index: -10;
	}
</style>
