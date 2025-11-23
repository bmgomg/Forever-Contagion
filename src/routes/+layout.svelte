<script>
	import favicon from '$lib/images/favicon.png';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

{@render children?.()}

<style>
	:global {
		body {
			margin: 0;
			overflow: hidden;
			--background: #000;
			background: var(--background);
			color: #fff;
			font-family: Quicksand;
		}

		.no-highlight {
			-webkit-tap-highlight-color: transparent;
			-webkit-touch-callout: none;
			-webkit-user-select: none;
			-khtml-user-select: none;
			-moz-user-select: none;
			-ms-user-select: none;
			user-select: none;
		}
	}

	@font-face {
		font-family: DMSans;
		src: url('$lib/fonts/DMSans.ttf');
	}

	@font-face {
		font-family: Orbitron;
		src: url('$lib/fonts/Orbitron.ttf');
	}

	@font-face {
		font-family: Radhiumz;
		src: url('$lib/fonts/NcsRadhiumz-Rp3x6.ttf');
	}
</style>
