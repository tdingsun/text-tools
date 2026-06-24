<script lang="ts">
	import { siteState } from '$lib/states.svelte';

	import { onMount } from 'svelte';
	import { RiTa } from 'rita';
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
	let stopChars = '.,?!;:';

	let currIdx = $state(0);
	let countIdx = $state(0);
	let countInterval = $state();
	onMount(() => {
		if (wordsArray) {
			currIdx = 0;
			countInterval = setInterval(() => {
				countIdx++;
			}, 250);
			setTimeout(nextWord, wordsArray[0].numSyllables * 250);
		}
	});
	const nextWord = () => {
		countIdx = 0;
		if (countInterval) {
			clearInterval(countInterval);
		}

		if (wordsArray && wordsArray.length > 0) {
			if (currIdx < wordsArray.length) {
				currIdx += 1;
			} else {
				currIdx = 0;
				countIdx = 0;
			}
		}
		let word = wordsArray[currIdx]?.word;
		let numSyllables = wordsArray[currIdx]?.numSyllables;
		if (numSyllables) {
			let time = numSyllables * 250;
			let lastChar = word[word.length - 1];
			if (stopChars.includes(lastChar)) {
				time += 250;
			}
			setTimeout(nextWord, time);
			countInterval = setInterval(() => {
				countIdx++;
			}, 250);
		} else {
			setTimeout(nextWord, 250);
		}
	};
</script>

{#if siteState.text}
	<div class="flex flex-col min-h-dvh justify-center items-center p-4">
		<div>{wordsArray[currIdx].word}</div>
		<div class="flex">
			{#each new Array(wordsArray[currIdx].numSyllables) as _, idx (idx)}
				<div
					class="border p-4 shrink-0 rounded-full {countIdx >= idx &&
					wordsArray[currIdx].numSyllables > 1
						? 'bg-black'
						: ''}"
				></div>
			{/each}
		</div>
	</div>
{/if}
