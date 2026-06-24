<script lang="ts">
	import { onMount } from 'svelte';

	let { char, speed = 1 } = $props();
	let xOffset = $state(0);
	let yOffset = $state(0);
	let halfSpeed = $derived(speed / 2);
	onMount(() => {
		setInterval(() => {
			xOffset += Math.random() * speed - halfSpeed;
			yOffset += Math.random() * speed - halfSpeed;
		}, 66);
	});

	const reset = () => {
		xOffset = 0;
		yOffset = 0;
	};
</script>

<span
	onmouseover={reset}
	style="transform: translate({xOffset}px, {yOffset}px);"
	class="inline-block min-w-1">{@html char}</span
>
