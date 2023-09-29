<script lang="ts">
	export let emoji: string;
	export let flipped: boolean;
	export let found: boolean;
</script>

<button class="square" class:flipped class:found disabled={found} on:click>
	{emoji}
</button>

<style>
	.square {
		background-color: white;
		border: 1px solid gray;
		display: grid;
		place-items: center;
		font-size: 4rem;
		cursor: pointer;
	}

	.flipped {
		background-color: lemonchiffon;
	}

	.found {
		background-color: lightgreen;
		cursor: default;
	}
</style>
