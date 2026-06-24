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
	let filter = $state('');

	const clear = () => {
		for (let i = 0; i < wordsArray.length; i++) {
			localStorage.removeItem(`cell.${i}`);
			let el: HTMLTextAreaElement = document.getElementById(`cell-${i}`);
			if (el && el.value) {
				el.value = '';
			}
		}
	};
</script>

{#if siteState.text}
	<div class="flex flex-col items-center">
		<div class="mb-4 flex gap-8">
			<div>
				<Button onclick={() => (filter = '')} class={filter === '' ? 'bg-green-100' : ''}
					>All</Button
				>
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
			</div>
			<div>
				<Button onclick={clear}>Clear</Button>
			</div>
		</div>

		<div class="flex flex-wrap shrink-0 w-full bg-gray-400 p-[0.5px] pt-0">
			{#each wordsArray as word, idx (idx)}
				<div
					class="shrink-0 basis-1/4 md:basis-1/5 lg:basis-1/6 xl:basis-1/8 p-[0.5px]
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
	</div>
{/if}
