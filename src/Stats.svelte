<script>
	import NumberFlow from '@number-flow/svelte';
	import { _stats, ss } from './state.svelte';
	import Timer from './Timer.svelte';

	const ave = $derived(_stats.won ? Math.round(_stats.total_ticks / _stats.won) : 0);
</script>

<div class="stats {ss.over ? 'over' : ''}" style="font-size: {Math.min(20, 22 * Math.min(ss.scale, 1))}px;">
	<div class="item">
		<span class="label">plays</span>
		<div class="flow"><NumberFlow value={_stats.plays} /></div>
	</div>
	<div class="item">
		<span class="label">completed</span>
		<div class="flow"><NumberFlow value={_stats.won} /></div>
	</div>
	<div class="item">
		<span class="label">ave</span>
		<div class="flow bold"><Timer ticks={ave} /></div>
	</div>
	<div class="item">
		<span class="label">longest</span>
		<div class="flow bold"><Timer ticks={_stats.best_ticks} /></div>
	</div>
</div>

<style>
	.stats {
		grid-area: 1/1;
		display: grid;
		grid-auto-flow: column;
		margin-top: 15px;
		place-self: center;
		gap: 20px;
	}

	.over {
		z-index: 3;
	}

	.item {
		border-radius: 50vh;
		display: grid;
		grid-auto-flow: column;
		gap: 10px;
		align-items: center;
		place-content: center;
	}

	.label {
		font-family: Orbitron;
	}

	.flow {
		font-family: Radhiumz;
		translate: 0 7%;
	}

	.bold {
		font-weight: bold;
	}
</style>
