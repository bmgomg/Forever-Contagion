<script>
	import { fade } from 'svelte/transition';
	import { ss } from './state.svelte';
	import { isZet, isPet } from './utils';
	import { random } from 'lodash-es';

	const { fob, src, style: imgStyle, scale = 1 } = $props();
	const { cx, cy, radius, tilt } = $derived(fob);
	const transition = $derived(ss.landing ? 'transform 1s, width 1s' : '');

	const style = $derived(
		`width: ${radius * 2}px; transform: translate(${cx - radius}px, ${cy - radius}px) scaleX(${scale}); transition: ${transition}; z-index: ${isZet(fob) ? 1 : 0};`
	);
</script>

<div class="fob" {style} transition:fade={{ duration: ss.over ? 500 : 0 }}>
	<div class="content {fob.shake ? 'shake' : ''}" style={`rotate: ${tilt || 0}deg; transition: rotate ${ss.over ? '1s' : '0.3s'}; ${imgStyle}`}>
		<img class={isPet(fob) ? 'pet' : ''} {src} alt="" style='animation-delay: {random(0,1)}s;'/>
	</div>
</div>

<style>
	.fob {
		grid-area: 1/1;
		display: grid;
		box-sizing: border-box;
		aspect-ratio: 1;
		border-radius: 50%;
		/* background: #fff7; */
		place-self: start;
	}

	.content {
		grid-area: 1/1;
		display: grid;
		border-radius: 50%;
	}

	img {
		grid-area: 1/1;
		box-sizing: border-box;
		border-radius: 50%;
		width: 100%;
		height: 100%;
		object-fit: cover;
		z-index: 1;
		transition:
			border-color 0.1s,
			opacity 1s;
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

	@keyframes spinner {
		from {
			transform: rotate(0deg);
		}
		to {
			transform: rotate(359deg);
		}
	}

	.pet {
		animation: pet 1.5s linear alternate infinite;
	}

	@keyframes pet {
		from {
			transform: rotate(-20deg);
		}
		to {
			transform: rotate(20deg);
		}
	}
</style>
