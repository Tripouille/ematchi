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
		transition: transform 0.5s;
	}

	img {
		transform: rotateY(180deg);
		transition: transform 0.5s;
		backface-visibility: hidden;
		position: absolute;
	}

	.flipped {
		background-color: lemonchiffon;
		transform: rotateY(180deg);
		& > img {
			transform: rotateY(0);
		}
	}

	.found {
		background-color: lightgreen;
	}
</style>
