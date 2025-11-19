<script>
	import NumberFlow from '@number-flow/svelte';
	import { ss } from './state.svelte';
	import Timer from './Timer.svelte';

	const duration = $derived('');

	const fsz = $derived(Math.min(32, 36 * Math.min(ss.scale, 1)));
	const lsz = $derived(fsz * 0.9);
	const alive = $derived(ss.fobs.filter(f => !f.dead).length);
</script>

{#if !ss.dlg}
	<div class="info-panel {ss.over ? 'over' : ''}" style="font-size: {fsz}px;">
		<div class="mid-section">
			<!-- <div class="label" style="font-size: {lsz}px;">{duration}</div> -->
			<div class="timer"><Timer /></div>
		</div>
		<div class="label" style="font-size: {lsz}px;">live kittens</div>
		<div class="comp">
			<NumberFlow value={alive} />
		</div>
	</div>
{/if}

<style>
	.info-panel {
		grid-area: 2/1;
		place-self: center;
		display: grid;
		place-items: center;
		/* background: #fff4; */
		padding: 10px;
		/* opacity: 0.3; */
		pointer-events: none;
		transition: opacity 1s;
	}

	.over {
		z-index: 2;
		/* opacity: 0.6; */
	}

	.mid-section {
		display: grid;
		place-items: center;
		margin: 15px 0;
	}

	.label {
		margin-right: 20px;
		font-family: Orbitron;
		font-weight: bold;
	}

	.timer,
	.comp {
		font-family: Radhiumz;
	}
</style>
