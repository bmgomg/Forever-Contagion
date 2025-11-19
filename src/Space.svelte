<script>
	import { onMount } from 'svelte';
	import { fade } from 'svelte/transition';
	import Zet from './Zet.svelte';
	import { doResize, loadGame } from './shared.svelte';
	import { ss } from './state.svelte';
	import Pet from './Pet.svelte';
	import { isPet, post } from './utils';

	onMount(() => {
		doResize();

		post(loadGame);
	});

	$effect(() => {
		const onResize = () => doResize(true);

		window.addEventListener('resize', onResize);
		return () => window.removeEventListener('resize', onResize);
	});
</script>

<div class="space {ss.dlg ? 'faded' : ss.restart ? 'hidden' : ''}">
	{#if ss.fobs.length}
		<div class="inner-space" transition:fade={{ duration: 2000 }}>
			<Zet />
			{#each ss.fobs.filter((f) => isPet(f)) as fob, index (fob.id)}
				<Pet {index} />
			{/each}
		</div>
	{/if}
</div>

<style>
	.space {
		grid-area: 1 / 1 / span 4/1;
		display: grid;
		transition: opacity 1s;
		box-sizing: border-box;
		/* border: 10px solid var(--lightblue); */
	}

	.inner-space {
		grid-area: 1/1;
		display: grid;
	}

	.faded {
		/* opacity: 0.25; */
		opacity: 0;
	}

	.hidden {
		opacity: 0;
	}
</style>
