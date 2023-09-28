<script>
	import Grid from "./Grid.svelte";
</script>

<div class="game">
    <div class="info">

    </div>

    <div class="grid-container">
        <Grid />
    </div>

    <div class="info">

    </div>
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