<script>
	import NumberFlow from '@number-flow/svelte';
	import { ss } from './state.svelte';
	import Timer from './Timer.svelte';
	import { liveCount } from './shared.svelte';

	const fsz = $derived(Math.min(32, 36 * Math.min(ss.scale, 1)));
	const lsz = $derived(fsz * 0.8);
</script>

{#if !ss.dlg}
	<div class="info-panel {ss.over ? 'over' : ''}" style="font-size: {fsz}px;">
		<div class="label" style="font-size: {lsz}px;">live kittens</div>
		<div class="num">
			<NumberFlow value={liveCount()} />
		</div>
		<div></div>
		<div class="label" style="font-size: {lsz}px;">{ss.over ? 'total contagion in' : 'mission duration'}</div>
		<div class="timer"><Timer ticks={ss.ticks} /></div>
	</div>
{/if}

<style>
	.info-panel {
		grid-area: 2/1;
		place-self: center;
		display: grid;
		place-items: center;
		gap: 5px;
		color: var(--lightblue);
		opacity: 0.7;
		pointer-events: none;
	}

	.over {
		z-index: 2;
		opacity: 0.9;
	}

	.label {
		font-family: Orbitron;
	}

	.timer,
	.num {
		font-family: Radhiumz;
		color: var(--green);
	}
</style>
