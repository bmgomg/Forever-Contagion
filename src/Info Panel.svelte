<script>
	import NumberFlow from '@number-flow/svelte';
	import { ss } from './state.svelte';
	// import Timer from './Timer.svelte';

	const fsz = $derived(Math.min(32, 36 * Math.min(ss.scale, 1)));
	const lsz = $derived(fsz * 0.8);
</script>

{#if !ss.dlg}
	<div class="info-panel" style="font-size: {fsz}px;">
		<!-- <div class="timer"><Timer ticks={ss.ticks} /></div> -->
		<div class="label" style="font-size: {lsz}px;">healthy kittens</div>
		<div class="num">
			<NumberFlow value={ss.fobs.filter((f) => !f.dead).length} />
		</div>
		<div class="label" style="font-size: {lsz}px;">plague-free time</div>
	</div>
{/if}

<style>
	.info-panel {
		grid-area: 2/1;
		place-self: center;
		display: grid;
		place-items: center;
		padding: 10px;
		color: var(--lightblue);
		opacity: 0.7;
		pointer-events: none;
	}

	.label {
		font-family: Orbitron;
		/* font-weight: bold; */
	}

	.timer,
	.num {
		font-family: Radhiumz;
	}

	.lives {
		display: grid;
		grid-auto-flow: column;
		align-items: center;
		gap: 10px;
	}
</style>
