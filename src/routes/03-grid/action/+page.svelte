<script lang="ts">
	import { gsap } from 'gsap/dist/gsap'
	import { Flip } from 'gsap/dist/Flip'

	gsap.registerPlugin(Flip)

	function flip(container: HTMLElement) {
		// get all grid items
		const gridItems = container.querySelectorAll('.grid-item')

		// the items are some cursed `NodeList` thing
		// you have to turn into a regular array
		for (let item of [...gridItems]) {
			item.addEventListener('click', () => {
				// if it contains `.details` do nothing
				if (item.classList.contains('details')) return

				// record the initial state
				const state = Flip.getState('.grid-item')

				// check for `.details` class and remove it
				const currentDetails = container.querySelector('.details')
				currentDetails && currentDetails.classList.remove('details')

				// show details
				item.classList.add('details')

				// flip
				const tl = Flip.from(state, {
					duration: 0.6,
					stagger: 0.04,
					absolute: true,
					onStart: () => {
						// fade out `.title`
						gsap.to('.title', {
							opacity: 0,
							y: '100%',
							duration: 0.3,
						})
					},
				})
				// fade in `.details .title`
				tl.to('.details .title', { opacity: 1, y: 0, duration: 0.3 })
			})
		}
	}
</script>

<div class="grid" use:flip>
	{#each { length: 8 } as _, id}
		{@const details = id === 0}
		{@const number = id + 1}

		<button class="grid-item" class:details>
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
