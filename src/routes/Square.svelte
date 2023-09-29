<script lang="ts">
	export let pokemonID: number;
	export let flipped: boolean;
	export let found: boolean;
</script>

<button class="square" class:flipped class:found disabled={found} on:click>
	<img height="100" width="100" src={`/svg/${pokemonID}.svg`} alt="" />
</button>

<style>
	.square {
		background-color: white;
		border: 1px solid gray;
		display: grid;
		place-items: center;
		font-size: 4rem;
		cursor: pointer;
		max-width: 100%;
		max-height: 100%;
	}

	.flipped {
		background-color: lemonchiffon;
	}

	.found {
		background-color: lightgreen;
		cursor: default;
	}
</style>
