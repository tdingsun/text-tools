<script lang="ts">
	import { browser } from '$app/env';
	import Button from '$lib/components/Button.svelte';
	import { siteState } from '$lib/states.svelte';
	import CloudWord from './CloudWord.svelte';
	let wordsArray = $derived(
		siteState.text
			.trim()
			.replaceAll(/[.,!?]+/g, '')
			.split(' ')
	);

	let showIdx = $state(false);
	let useLetters = $state(false);
</script>

{#if browser && siteState.text}
	<div class="flex-col justify-center items-center">
		<div class='flex justify-center gap-1'>
			<Button onclick={() => (showIdx = !showIdx)} class="border">Show Number</Button>
			<Button onclick={() => (useLetters = !useLetters)} class="border">{useLetters ? 'Split by Words' : 'Split by Letters'}</Button>
		</div>
		<div class="w-dvw h-dvh p-12 relative">
			<div class="relative w-full h-full">
				{#each wordsArray as word, idx (idx)}
					{#if useLetters}
						{#each word as letter, letterIdx (letterIdx)}
							<CloudWord word={letter} {idx} {showIdx}></CloudWord>
						{/each}
					{:else}
						<CloudWord {word} {idx} {showIdx}></CloudWord>
					{/if}
				{/each}
			</div>
		</div>
	</div>
{/if}
