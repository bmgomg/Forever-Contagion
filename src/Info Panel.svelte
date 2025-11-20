<script>
	import NumberFlow from '@number-flow/svelte';
	import { ss } from './state.svelte';
	import Timer from './Timer.svelte';

	const fsz = $derived(Math.min(32, 36 * Math.min(ss.scale, 1)));
	const lsz = $derived(fsz * 0.9);
	const lives = $derived(() => ss.fobs.reduce((sum, f) => sum + (f.lives || 0), 0));
</script>

{#if !ss.dlg}
	<div class="info-panel {ss.over ? 'over' : ''}" style="font-size: {fsz}px;">
		<div class="timer"><Timer ticks={ss.ticks} /></div>
		<div class="lives">
			<div class="label" style="font-size: {lsz}px;">lives:</div>
			<div class="num">
				<NumberFlow value={ss.fobs.reduce((sum, f) => sum + (f.lives || 0), 0)} />
			</div>
		</div>
	</div>
{/if}

<style>
	.info-panel {
		grid-area: 2/1;
		place-self: center;
		display: grid;
		place-items: center;
		gap: 20px;
		pointer-events: none;
	}

	.over {
		z-index: 2;
	}

	.label {
		font-family: Radhiumz;
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
