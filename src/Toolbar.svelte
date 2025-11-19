<script>
	import { fade } from 'svelte/transition';
	import { _sound } from './sound.svelte';
	import { ss } from './state.svelte';

	const orange = '<span style="font-weight: bold;">';
	const PAUSE = `<span>pause/instructions  ${orange}ESC</span></span>`;
	const TOOLS = $derived(
		`<span>sfx ${_sound.sfx ? 'on' : 'off'}  ${orange}S</span>   music ${_sound.music ? 'on' : 'off'}  ${orange}M</span>   reset stats  ${orange}Z</span></span>`
	);
	const style = $derived(`font-size: ${Math.min(20, 22 * Math.min(ss.scale, 1))}px;`);
</script>

<div class="toolbar {ss.over ? 'over' : ''}" {style}>
	{#if ss.dlg}
		<span class="tools" transition:fade>{@html TOOLS}</span>
	{:else}
		<span class="pause" transition:fade>{@html PAUSE}</span>
	{/if}
</div>

<style>
	.toolbar {
		display: grid;
		place-items: center;
		outline: none !important;
		font-family: Orbitron;
	}

	.over {
		z-index: 3;
	}

	.tools {
		grid-area: 1/1;
		/* opacity: 0.6; */
	}

	.pause {
		grid-area: 1/1;
		/* opacity: 0.6; */
	}
</style>
