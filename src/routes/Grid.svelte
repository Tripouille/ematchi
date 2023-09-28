<script>
	import Square from "./Square.svelte";
</script>

<div class="grid">
    {#each Array(16) as _}
        <Square />
    {/each}
</div>

<style>
    .grid {
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        grid-template-rows: repeat(4, 1fr);
        gap: 0.2rem;
        height: 100%;
        padding: 0.2rem;
    }
</style>