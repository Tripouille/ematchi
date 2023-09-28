<script lang="ts">
	import Grid from './Grid.svelte';
	import { levels, type Level } from './levels.js';

	const currentLevelLabel: Level['label'] = 'easy';

	let size: number;
	let grid: string[] = [];

	function initializeGame(levelLabel: Level['label']) {
		const level = levels.find((l) => l.label === levelLabel);
		if (!level) throw new Error(`Level ${levelLabel} not found`);

		size = level.size;

        const pairs: string[] = [];
		const emojisCopy = [...level.emojis];
		for (let i = 0; i < level.size ** 2 / 2; i++) {
			const randomIndex = Math.floor(Math.random() * emojisCopy.length);
			pairs.push(emojisCopy[randomIndex]);
			emojisCopy.splice(randomIndex, 1);
		}
		pairs.push(...pairs);
		grid = pairs.sort(() => Math.random() - 0.5);
	}
	initializeGame(currentLevelLabel);
</script>

<div class="game">
	<div class="info" />

	<div class="grid-container">
		<Grid {grid} />
	</div>

	<div class="info" />
</div>

<style>
	.game {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}

	.info {
		width: 80vmin;
		aspect-ratio: 8;
		max-width: 700px;
		background-color: teal;
	}

	.grid-container {
		width: 80vmin;
		aspect-ratio: 1;
		max-width: 700px;
		background-color: teal;
	}
</style>
