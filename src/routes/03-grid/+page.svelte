<script lang="ts">
	import { tick } from 'svelte'
	import { gsap } from 'gsap/dist/gsap'
	import { Flip } from 'gsap/dist/Flip'

	gsap.registerPlugin(Flip)

	// selected image
	let selected = 0

	async function flip(id: number) {
		// record the initial state
		const state = Flip.getState('.grid-item')

		// change selected image
		selected = id

		// wait for DOM updates
		await tick()

		// flip
		const tl = Flip.from(state, {
			duration: 0.6,
			stagger: 0.04,
			absolute: true,
			onStart: () => {
				// fade out
				gsap.to('.title', {
					opacity: 0,
					y: '100%',
					duration: 0.3,
				})
			},
		})
		// fade in
		tl.to('.details .title', { opacity: 1, y: 0, duration: 0.3 })
	}
</script>

<div class="grid">
	{#each { length: 8 } as _, id}
		{@const details = selected === id}
		{@const number = id + 1}

		<button class="grid-item" class:details on:click={() => flip(id)}>
			<div class="title">
				<h1>Image {number}</h1>
			</div>
			<img src="https://picsum.photos/600/600?random={id}" alt="Placeholder" />
		</button>
	{/each}
</div>

<style>
	.grid {
		display: grid;
		gap: 1rem;
		grid-template-columns: repeat(2, 1fr);
	}

	@media (min-width: 1024px) {
		.grid {
			grid-template-columns: repeat(3, 1fr);
		}
	}

	.grid-item {
		position: relative;
		padding: 0;
		background: none;
		border: none;
		overflow: hidden;
		cursor: pointer;
	}

	h1 {
		color: hsl(0 0% 98%);
		font-size: 2rem;
		text-transform: capitalize;
	}

	img {
		width: 100%;
		height: 100%;
		aspect-ratio: 16/9;
		display: block;
		object-fit: cover;
		border-radius: 4px;
	}

	.details {
		grid-row: span 2;
		grid-column: span 2;
	}

	.title {
		position: absolute;
		left: 20px;
		bottom: 0px;
		opacity: 0;
		translate: 0% 100%;
	}

	.details .title {
		opacity: 1;
		translate: 0%;
	}
</style>
