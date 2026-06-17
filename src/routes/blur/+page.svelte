<script lang="ts">
	import { siteState } from '$lib/states.svelte';
	let wordsArray = $derived(
		siteState.text
			.trim()
			.replaceAll(/[.,!?]+/g, '')
			.split(' ')
	);
    let numButtons = new Array(10)
    let mod = $state(1);
</script>

{#if siteState.text}
    {#each numButtons as _, idx (idx)}
        <button onclick={() => mod = idx + 1} class="border p-4">{idx + 1}</button>
    {/each}
    

	<div class="flex justify-center">
		<div class="p-4 max-w-lg">
			{#each wordsArray as word, idx (idx)}
				<span class="{idx % mod === 0 ? '' : 'blur-xs' }">
					{word.toLowerCase()}
				</span>
				<span> </span>
			{/each}
		</div>
	</div>
{/if}
