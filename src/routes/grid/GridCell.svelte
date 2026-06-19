<script lang="ts">
	import Button from '$lib/components/Button.svelte';
	import { onMount } from 'svelte';

	let { word, idx } = $props();
	let value = $state('');

	let storeValue = () => {};
</script>

<div class="flex flex-col items-center bg-white p-2 gap-2">
	<div class="flex w-full justify-between text-xs {value ? '' : 'text-gray-400'}">
		<div class="text-xs">
			{idx + 1}
		</div>
		<div>{word.toLowerCase()}</div>
	</div>

	<textarea
		onchange={storeValue}
		bind:value
		class="w-full field-sizing-content max-w-full resize-none wrap-anywhere"></textarea>
</div>
