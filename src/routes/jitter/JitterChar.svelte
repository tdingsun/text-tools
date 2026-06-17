<script lang="ts">
	import { onMount } from 'svelte';

	let { char } = $props();
	let xOffset = $state(0);
	let yOffset = $state(0);
	onMount(() => {
		setInterval(() => {
			xOffset += Math.random() * 1 - 0.5;
			yOffset += Math.random() * 1 - 0.5;
		}, 66);
	});

	const reset = () => {
		xOffset = 0;
		yOffset = 0;
	};
</script>

<span onmouseover={reset} style="transform: translate({xOffset}px, {yOffset}px);" class="inline-block min-w-1"
	>{char}</span
>
