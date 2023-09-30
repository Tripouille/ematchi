<script lang="ts">
	import '../styles.css';
	import Game from './Game.svelte';
	import Modal from './Modal.svelte';

	let state: 'waiting' | 'playing' | 'paused' | 'won' | 'lost' = 'paused';
</script>

<Game />

{#if state !== 'playing'}
	<Modal>
		<h1><span>Poke</span>match</h1>
		{#if state === 'waiting'}
			<h2>Choose a level</h2>
		{:else if state === 'paused'}
			<h2>Paused</h2>
		{:else if state === 'won' || state === 'lost'}
			you {state} the game
		{/if}

		<div class="buttons">
			{#if state === 'paused'}
				<button on:click={() => (state = 'playing')}>Resume</button>
			{/if}
		</div>
	</Modal>
{/if}
