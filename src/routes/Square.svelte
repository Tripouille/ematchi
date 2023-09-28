<script lang="ts">
	export let emoji: string;
</script>

<div class="square">
	{emoji}
</div>

<style>
	.square {
		background-color: lightcyan;
		border: 1px solid gray;
		display: grid;
		place-items: center;
		font-size: 4rem;
	}
</style>
