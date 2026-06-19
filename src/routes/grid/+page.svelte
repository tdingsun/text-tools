<script lang="ts">
	import Button from '$lib/components/Button.svelte';
	import { siteState } from '$lib/states.svelte';
	import { RiTa } from 'rita';
	import GridCell from './GridCell.svelte';
	let wordsArray = $derived(
		siteState.text
			.trim()
			.replaceAll(/[.,!?]+/g, '')
			.split(' ')
	);
	let partsOfSpeech = $derived(RiTa.pos(wordsArray, { simple: true }));
	console.log(partsOfSpeech);
	let filter = $state('');
</script>

{#if siteState.text}
	<div class="mb-4">
		<Button onclick={() => (filter = 'n')} class={filter === 'n' ? 'bg-green-100' : ''}
			>Nouns</Button
		>
		<Button onclick={() => (filter = 'a')} class={filter === 'a' ? 'bg-green-100' : ''}
			>Adjectives</Button
		>
		<Button onclick={() => (filter = 'v')} class={filter === 'v' ? 'bg-green-100' : ''}
			>Verbs</Button
		>
		<Button onclick={() => (filter = 'r')} class={filter === 'r' ? 'bg-green-100' : ''}
			>Adverbs</Button
		>
		<Button onclick={() => (filter = '')} class={filter === '' ? 'bg-green-100' : ''}>All</Button>
	</div>

	<div class="flex flex-wrap bg-gray-400 p-[0.5px] pt-0">
		{#each wordsArray as word, idx (idx)}
			<div
				class="basis-1/4 md:basis-1/5 lg:basis-1/6 xl:basis-1/8 p-[0.5px]
				{filter === 'n' && partsOfSpeech[idx] !== 'n' ? 'hidden' : ''}
				{filter === 'a' && partsOfSpeech[idx] !== 'a' ? 'hidden' : ''}
				{filter === 'v' && partsOfSpeech[idx] !== 'v' ? 'hidden' : ''}
				{filter === 'r' && partsOfSpeech[idx] !== 'r' ? 'hidden' : ''}
				"
			>
				<GridCell {word} {idx}></GridCell>
			</div>
		{/each}
	</div>
{/if}
