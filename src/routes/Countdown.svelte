<script lang="ts">
	export let remaining: number;
	export let duration: number;
</script>

<div class="countdown">
	<button>
		<svg fill="gray" height="60" width="60" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
			<title>pause</title>
			<path
				d="M15,16H13V8H15M11,16H9V8H11M12,2A10,10 0 0,0 2,12A10,10 0 0,0 12,22A10,10 0 0,0 22,12A10,10 0 0,0 12,2Z"
			/>
		</svg>
	</button>

	<div class="bar" style="--remaining: {remaining / duration}">
		<div class="duration" />
		<div class="remaining" />
	</div>
</div>

<style lang="scss">
	.countdown {
		display: flex;
		gap: 1rem;
		justify-content: center;
		align-items: center;
	}

	button {
		border: none;
		padding: 0;
		cursor: pointer;
		display: inline-grid;
		background: transparent;
	}

	.bar {
		flex: 1;
		position: relative;
		height: 0.5rem;

		* {
			height: 100%;
			width: 100%;
			border-radius: 0.25rem;
			position: absolute;
		}

		.remaining {
			background: gray;
			width: calc(var(--remaining) * 100%);
		}

		.duration {
			background: lightgray;
		}
	}
</style>
