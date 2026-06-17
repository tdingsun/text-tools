<script lang="ts">
	import { onMount } from 'svelte';

	let { word, idx, showIdx } = $props();
	let x = $state(0);
	let y = $state(0);
	onMount(() => {
		x = Math.random() * 100;
		y = Math.random() * 100;
	});

	const onMouseOver = () => {
		x += Math.random() * 10 - 5;
		y += Math.random() * 10 - 5;
	};
</script>

<div
	onmouseover={onMouseOver}
	style="left: {x}%; top: {y}%;"
	class="absolute transition-[left,top] duration-250"
>
	<div class="flex flex-col items-center text-center -translate-x-1/2 -translate-y-1/2">
		<div class="text-sm">{word.toLowerCase()}</div>
		{#if showIdx}
			<div class="text-[8px] w-5 h-5 flex justify-center items-center rounded-full">
				{idx + 1}
			</div>
		{/if}
	</div>
</div>
