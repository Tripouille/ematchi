<script lang="ts">
	import { send } from './transitions';

	export let pokemonID: number;
	export let flipped: boolean;
	export let found: boolean;
	export let group: 'a' | 'b';
</script>

<div class="square" class:flipped={flipped || found}>
	<button on:click disabled={flipped || found} />

	{#if !found}
		<img
			height="150"
			width="150"
			alt=""
			src={`/svg/${pokemonID}.svg`}
			out:send={{ key: `${pokemonID}-${group}` }}
		/>
	{/if}
</div>

<style>
	.square {
		display: grid;
		place-items: center;
		transition: filter 0.2s;
		transform-style: preserve-3d;
		transform: rotateY(180deg);
		transition: transform 0.4s;
		border: 1px solid gray;
		border-radius: 1rem;
	}

	.square * {
		backface-visibility: hidden;
	}

	button {
		position: absolute;
		width: 100%;
		height: 100%;
		border: none;
		display: flex;
		justify-content: center;
		align-items: center;
		background: lemonchiffon;
		border-radius: 1em;
		transform: rotateY(180deg);
		-webkit-tap-highlight-color: transparent;
		cursor: pointer;
	}

	button:disabled {
		color: inherit;
	}

	.flipped {
		transform: none;
	}

	img {
		width: 100%;
		height: 100%;
		aspect-ratio: 1;
		padding: 1rem;
		object-fit: contain;
	}
</style>
