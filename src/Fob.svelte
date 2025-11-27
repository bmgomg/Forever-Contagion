<script>
	import { random } from 'lodash-es';
	import { fade } from 'svelte/transition';
	import { DEAD_MS, TICK_MS, ZET_VELOCITY_DELTA } from './const';
	import { ss } from './state.svelte';
	import { isZet } from './utils';

	const { fob, src, scale = 1 } = $props();
	const { cx, cy, radius } = $derived(fob);
	const transition = $derived(ss.landing ? 'transform 1s, width 1s' : '');

	const style = $derived(
		`width: ${radius * 2}px; transform: translate(${cx - radius}px, ${cy - radius}px) scaleX(${scale}); transition: ${transition}; z-index: ${isZet(fob) ? 1 : 0};`
	);
</script>

<div class="fob" {style} transition:fade={{ duration: ss.over ? 500 : 0 }}>
	<div class="shakeable {fob.shake ? 'shake' : ''}">
		<div class="rotatable {fob.dead ? '' : 'alive'}" style="animation-delay: {random(0, 1)}s;">
			<img {src} alt="" />
		</div>
	</div>
	{#if isZet(fob)}
		{@const { x, y } = fob.vel}
		{#if false}
			{@const w = radius * 0.25}
			{@const off = radius * 1.3}
			{@const _x = Math.abs(x).toFixed(1) * 2}
			{@const _y = Math.abs(y).toFixed(1) * 2}
			{#if _x}
				<div class="vel" style="width: ${w}px; translate: {x > 0 ? off : -off}px 0;">{_x}</div>
			{/if}
			{#if _y}
				<div class="vel" style="width: ${w}px; translate: 0 {(y > 0 ? off : -off) * 1.1}px;">{_y}</div>
			{/if}
		{/if}
		{#if !ss.over}
			{#each [1, 2, 3, 4, 5, 6] as i}
				{@const threshold = i * ZET_VELOCITY_DELTA * ss.scale}
				{@const w = radius * 1 * (1 - i * 0.05)}
				{@const off = 4 * (i + 1)}
				{#if Math.abs(x).toFixed(1) >= threshold}
					{@const cls = x < 0 ? 'wave-x-r' : 'wave-x-l'}
					<div class={cls} style="width: {w}px; translate: {off * (x < 0 ? 1 : -1)}px 0;"></div>
				{/if}
				{#if Math.abs(y).toFixed(1) >= threshold}
					{@const cls = y < 0 ? 'wave-y-b' : 'wave-y-t'}
					<div class={cls} style="width: {w}px; translate: 0 {off * (y < 0 ? 1 : -1)}px;"></div>
				{/if}
			{/each}
		{/if}
	{:else if fob.dead && false}
		{@const secs = Math.round((DEAD_MS - (ss.ticks - fob.dead) * TICK_MS) / 1000)}
		{#if secs > 0}
			<div class="secs">
				{secs}
			</div>
		{/if}
	{/if}
</div>

<style>
	.fob {
		grid-area: 1/1;
		display: grid;
		box-sizing: border-box;
		aspect-ratio: 1;
		place-self: start;
	}

	.shakeable {
		grid-area: 1/1;
		display: grid;
		border-radius: 50%;
	}

	.rotatable {
		display: grid;
	}

	img {
		grid-area: 1/1;
		box-sizing: border-box;
		width: 100%;
		height: 100%;
		object-fit: cover;
	}

	.shake {
		animation: shake 0.1s 6 linear;
	}

	@keyframes shake {
		from {
			transform: scale(1, 1);
		}
		33% {
			transform: scale(1, 1.2);
		}
		66% {
			transform: scale(1.2, 1);
		}
		to {
			transform: scale(1, 1);
		}
	}

	.alive {
		animation: alive 1.5s linear alternate infinite;
	}

	@keyframes alive {
		from {
			transform: rotate(-30deg);
		}
		to {
			transform: rotate(30deg);
		}
	}

	.vel {
		grid-area: 1/1;
		place-self: center;
		font-size: 18px;
		display: grid;
		place-content: center;
	}

	.secs {
		grid-area: 1/1;
		place-self: start;
		font-size: 18px;
		display: grid;
		color: gold;
		font-weight: bold;
	}

	.wave-x-l,
	.wave-x-r,
	.wave-y-t,
	.wave-y-b {
		grid-area: 1/1;
		place-self: center;
		display: grid;
		border: 1px solid transparent;
		border-radius: 50%;
		aspect-ratio: 1;
	}

	.wave-x-l {
		justify-self: start;
		border-left-color: var(--green);
	}

	.wave-x-r {
		justify-self: end;
		border-right-color: var(--green);
	}

	.wave-y-t {
		align-self: start;
		border-top-color: var(--green);
	}

	.wave-y-b {
		align-self: end;
		border-bottom-color: var(--green);
	}
</style>
