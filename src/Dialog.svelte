<script>
	import { fade } from 'svelte/transition';
	import { ss } from './state.svelte';

	const ul = '<ul style="margin: 25px 0 0 0;">';
	const li = '<li style="margin: 12px 0 0 -20px; color: var(--orange);">';

	const CONTENT = `
        <span style='font-style: italic;'>You are a self-aware zombie kitten drifting through space, trying not to infect the innocent. The inevitable cannot be stopped—but it can be delayed.</span>
        ${ul}
        ${li}<span>Use arrow keys to adjust your velocity—horizontal or vertical.  Speed increases are capped.</span></li>
        ${li}<span>Touching a live kitten turns it into a permanent zombie.</span></li>
        ${li}<span>Infected kittens spread the plague, but their infections are temporary.</span></li>
        ${li}<span>Keep at least one kitten alive.</span></li>
        </ul>`;

	const width = $derived(ss.space?.width > 580 ? '540px' : '80%');
	const style = $derived(`width: ${width}; font-size: ${Math.min(24, 30 * Math.min(ss.scale, 1))}px;`);
</script>

{#if ss.dlg}
	<div class="dlg" {style} transition:fade={{ duration: 200 }}>
		<div class="content" tabindex="-1">
			{@html CONTENT}
		</div>
	</div>
{/if}

<style>
	.dlg {
		grid-area: 2/1;
		display: grid;
		place-self: center;
		box-sizing: border-box;
		place-items: center;
		margin: 20px 0;
	}

	.content {
		/* font-weight: bold; */
		display: grid;
		align-content: start;
		place-self: center;
		outline: none !important;
	}
</style>
