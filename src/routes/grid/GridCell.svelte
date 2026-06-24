<script lang="ts">
	import Button from '$lib/components/Button.svelte';
	import { onMount } from 'svelte';

	let { word, idx } = $props();
	let value = $state('');

	onMount(() => {
		let storedValue = localStorage.getItem(`cell.${idx}`);
		if (storedValue) {
			value = storedValue;
		}
	});

	let storeValue = () => {
		localStorage.setItem(`cell.${idx}`, value);
	};
</script>

<div class="flex flex-col items-center bg-white p-2 gap-2">
	<div class="flex w-full justify-between">
		<div class="text-xs">{word.toLowerCase()}</div>

		<div class="text-xs">
			{idx + 1}
		</div>
	</div>

	<textarea
		id="cell-{idx}"
		onchange={storeValue}
		bind:value
		class="w-full field-sizing-content max-w-full resize-none wrap-anywhere"></textarea>
</div>
