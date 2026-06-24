<script lang="ts">
	import { siteState } from '$lib/states.svelte';

	import { onMount } from 'svelte';
	import { RiTa } from 'rita';
	import Button from '$lib/components/Button.svelte';
	let wordsArray = $derived(
		siteState.text
			.trim()
			.split(' ')
			.map((word) => {
				return {
					word: word,
					numSyllables: RiTa.syllables(word).split('/').length
				};
			})
	);
	let concordance = $state({});
	let concordanceSorted = $state([]);
	let kwic = $state({});
	$effect(() => {
		concordance = RiTa.concordance(siteState.text, {
			ignoreCase: true,
			ignorePunctuation: true,
			ignoreStopWords: true
		});
	});
	$effect(() => {
		concordanceSorted = Object.entries(concordance).sort(([wordA, freqA], [wordB, freqB]) => {
			return freqB - freqA;
		});
	});

	let lines = $state([]);
	let clickedWord = $state('');

	const getKWIC = (word) => {
		clickedWord = word;
		lines = RiTa.kwic(word, { numWords: 3 });
	};
</script>

{#if siteState.text}
	<div class="flex p-4">
		<div class="flex flex-col gap-2 items-center overflow-auto max-h-[calc(100dvh-12rem)] pr-8">
			{#each concordanceSorted as [word, freq], idx (idx)}
				<div class="flex gap-4 items-stretch w-full">
					<Button onclick={() => getKWIC(word)} class="w-full">
						<div class="flex justify-between gap-4">
							<span>
								{word}
							</span>
							<span>
								{freq}
							</span>
						</div>
					</Button>
				</div>
			{/each}
		</div>
		<div>
			{#if lines}
				<div class="flex flex-col">
					{#each lines as line, idx (idx)}
						<div>
							{#each line.split(' ') as word, idx (idx)}
								<span
									class={word.toLowerCase().replaceAll(/[.,!?]+/g, '') === clickedWord.toLowerCase()
										? 'text-red-400'
										: ''}>{word}</span
								>
								<span> </span>
							{/each}
						</div>
					{/each}
				</div>
			{/if}
		</div>
	</div>
{/if}
