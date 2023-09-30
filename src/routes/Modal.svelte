<script lang="ts">
</script>

<div class="modal-background">
	<div class="content">
		<slot />
	</div>
</div>

<style>
	.modal-background {
		position: fixed;
		inset: 0;
		backdrop-filter: blur(10px);
		display: grid;
		place-items: center;
		z-index: 999;
	}
</style>
