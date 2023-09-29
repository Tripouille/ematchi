<script lang="ts">
	import { onMount } from 'svelte';
	import Countdown from './Countdown.svelte';
	import Grid from './Grid.svelte';
	import { levels, type Level } from './levels.js';

	const currentLevelLabel: Level['label'] = 'easy';

	let grid: string[] = [];

	function initializeGame(levelLabel: Level['label']) {
		const level = levels.find((l) => l.label === levelLabel);
		if (!level) throw new Error(`Level ${levelLabel} not found`);

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
			requestAnimationFrame(loop);
			remaining = duration - (Date.now() - startDate) / 1000;
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
		{#each foundedEmoji as emoji}
			{emoji}
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
