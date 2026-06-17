<script lang="ts">
	import JitterChar from './JitterChar.svelte';
	import { siteState } from '$lib/states.svelte';
	let charArray = $derived(siteState.text.trim().split(''));
</script>

{#if siteState.text}
	<div class="flex flex-wrap p-4 justify-center items-center">
		<div class="max-w-lg">
			{#each charArray as char, idx (idx)}
				<JitterChar {char}></JitterChar>
			{/each}
		</div>
	</div>
{/if}
