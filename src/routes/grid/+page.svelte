<script lang="ts">
	import { siteState } from '$lib/states.svelte';
	let wordsArray = $derived(
		siteState.text
			.trim()
			.replaceAll(/[.,!?]+/g, '')
			.split(' ')
	);
</script>

{#if siteState.text}
	<div class="flex flex-wrap bg-black p-[0.5px] pt-0">
		{#each wordsArray as word, idx (idx)}
			<div class="basis-1/8 p-[0.5px]">
				<div class="flex flex-col items-center bg-white py-4 px-2">
					<div class="text-sm">{word.toLowerCase()}</div>
					<div class="text-xs">
						{idx + 1}
					</div>
				</div>
			</div>
		{/each}
	</div>
{/if}
