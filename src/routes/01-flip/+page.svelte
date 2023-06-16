<script lang="ts">
	import { tick } from 'svelte'

	// stable reference to the circle element
	let circleEl: HTMLDivElement

	async function flip() {
		// get the FIRST position
		const first = circleEl.getBoundingClientRect()

		// make change
		swap = !swap

		// wait for DOM updates to be applied
		await tick()

		// get the LAST position
		const last = circleEl.getBoundingClientRect()

		// INVERT position
		const invert = first.left - last.left

		// PLAY from the inverted position to last
		const animation = circleEl.animate(
			[
				{ translate: `${invert}px` },
				{ translate: '0px', background: 'yellow' },
			],
			{
				duration: 2000,
				fill: 'forwards',
				easing: 'ease-out',
			}
		)
	}

	let swap = false
</script>

<h1>Click anywhere to FLIP</h1>

<svelte:document on:click={flip} />

<div class="container">
	<div class="parent">
		{#if !swap}
			<div bind:this={circleEl} class="circle">First</div>
		{/if}
	</div>

	<div class="parent">
		{#if swap}
			<div bind:this={circleEl} class="circle">Last</div>
		{/if}
	</div>
</div>

<style>
	h1 {
		position: absolute;
		top: 10%;
		left: 50%;
		translate: -50%;
		text-transform: capitalize;
	}

	.container {
		height: 100vh;
		display: grid;
		grid-template-columns: repeat(2, 1fr);
		place-items: center;
		cursor: pointer;
	}

	.parent {
		width: 300px;
		aspect-ratio: 1;
		display: grid;
		place-content: center;
		border: 2px dashed hsl(220 10% 40%);
		border-radius: 4px;
	}

	.circle {
		width: 100px;
		border-radius: 50%;
		aspect-ratio: 1;
		display: grid;
		place-content: center;
		color: hsl(0 0% 0%);
		background-color: aqua;
	}
</style>
