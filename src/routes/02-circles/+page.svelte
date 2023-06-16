<script lang="ts">
	import { tick } from 'svelte'
	import { gsap } from 'gsap/dist/gsap'
	import { Flip } from 'gsap/dist/Flip'

	gsap.registerPlugin(Flip)

	async function flip() {
		// get initial state
		const state = Flip.getState('.circle', { props: 'borderRadius' })

		// change layout
		layout === 'grid' ? (layout = 'stack') : (layout = 'grid')

		// wait for changes to DOM
		await tick()

		// flip
		Flip.from(state, {
			duration: 0.6,
			absolute: true,
			scale: true,
			stagger: -0.1,
			spin: true,
			ease: 'power1.easeOut',
		})
	}

	type Layout = 'stack' | 'grid'

	let layout: Layout = 'stack'
</script>

<svelte:window on:click={flip} />

<h1>Click anywhere to FLIP</h1>

<div class="container">
	<div data-layout={layout}>
		{#each { length: 10 } as _, id}
			<img
				class="circle"
				src="https://picsum.photos/100/100?random={id}"
				alt="Placeholder"
			/>
		{/each}
	</div>
</div>

<style>
	h1 {
		position: absolute;
		top: 20%;
		left: 50%;
		translate: -50%;
		text-transform: capitalize;
	}

	.container {
		height: 100vh;
		display: grid;
		place-content: center;
		cursor: pointer;
	}

	.circle {
		width: 100px;
		aspect-ratio: 1;
		border-radius: 50%;
		border: 4px solid hsl(220 10% 10%);
	}

	[data-layout='stack'] {
		display: flex;
	}

	[data-layout='stack'] .circle:not(:first-child) {
		margin-left: -40px;
	}

	[data-layout='grid'] {
		display: grid;
		grid-template-columns: repeat(5, 1fr);
		gap: 0.5rem;
	}

	[data-layout='grid'] .circle {
		border-radius: 20%;
	}
</style>
