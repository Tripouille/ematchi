<script lang="ts">
	import { onMount } from 'svelte';
	import Countdown from './Countdown.svelte';
	import Grid from './Grid.svelte';
	import { levels, type Level } from './levels.js';

	const currentLevelLabel: Level['label'] = 'easy';

	let grid: number[] = [];

	function initializeGame(levelLabel: Level['label']) {
		const level = levels.find((l) => l.label === levelLabel);
		if (!level) throw new Error(`Level ${levelLabel} not found`);

		const pairs: number[] = [];
		for (let i = 0; i < level.size ** 2 / 2; i++) {
			let randomIndex;

			do {
				randomIndex = Math.ceil(Math.random() * 200);
			} while (pairs.includes(randomIndex));

			pairs.push(randomIndex);
		}
		pairs.push(...pairs);
		grid = pairs.sort(() => Math.random() - 0.5);
	}
	initializeGame(currentLevelLabel);

	let foundedEmoji: string[] = [];
	function handleEmojiFound(event: any) {
		foundedEmoji = foundedEmoji.concat(event.detail.emoji as string);
	}

	const duration = 30.0;
	let remaining = 30.0;

	function startGame() {
		const startDate = Date.now();

		function loop() {
			if (remaining <= 0) return;
			remaining = duration - (Date.now() - startDate) / 1000;
			requestAnimationFrame(loop);
		}
		loop();
	}

	onMount(startGame);
</script>

<div class="game">
	<div class="info">
		<Countdown {duration} {remaining} />
	</div>

	<div class="grid-container">
		<Grid {grid} on:emoji-found={handleEmojiFound} />
	</div>

	<div class="info" />
	<p>
		{#each foundedEmoji as pokemonID}
			<img height="100" width="100" src={`/svg/${pokemonID}.svg`} alt="" />
		{/each}
	</p>
</div>

<style>
	.game {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		border-radius: 1rem;
	}

	.info {
		width: 80vmin;
		aspect-ratio: 8;
		max-width: 700px;
	}

	.grid-container {
		width: 80vmin;
		aspect-ratio: 1;
		max-width: 700px;
	}
</style>
