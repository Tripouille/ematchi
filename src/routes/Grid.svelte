<script lang="ts">
	import { createEventDispatcher } from 'svelte';
	import Square from './Square.svelte';

	const dispatcher = createEventDispatcher();

	export let grid: string[];
	let foundedSquareIndexes: number[] = [];
	let flippedSquareIndexes: number[] = [];
	let timeoutID: number;

	function flipSquare(index: number) {
		if (flippedSquareIndexes.length >= 2) {
			clearTimeout(timeoutID);
			flippedSquareIndexes = [];
		}

		flippedSquareIndexes = flippedSquareIndexes.concat(index);

		if (flippedSquareIndexes.length === 2) {
			const [firstIndex, secondIndex] = flippedSquareIndexes;
			if (grid[firstIndex] === grid[secondIndex]) {
				dispatcher('emoji-found', { emoji: grid[firstIndex] });
				foundedSquareIndexes = foundedSquareIndexes.concat(flippedSquareIndexes);
			}
			timeoutID = setTimeout(() => {
				flippedSquareIndexes = [];
			}, 1000);
		}
	}
</script>

<div class="grid">
	{#each grid as emoji, i}
		<Square
			{emoji}
			on:click={() => flipSquare(i)}
			flipped={flippedSquareIndexes.includes(i)}
			found={foundedSquareIndexes.includes(i)}
		/>
	{/each}
</div>

<style>
	.grid {
		display: grid;
		grid-template-columns: repeat(4, 1fr);
		grid-template-rows: repeat(4, 1fr);
		gap: 0.2rem;
		height: 100%;
		padding: 0.2rem;
	}
</style>
