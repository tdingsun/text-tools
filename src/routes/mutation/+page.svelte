<script lang="ts">
	import { siteState } from '$lib/states.svelte';
	import { RiTa } from 'rita';
	let wordsArray = $derived(siteState.text.trim().split(' '));
	let mutatedCopy = $state(
		wordsArray.map((word) => {
			return {
				word: word,
				isMutated: false
			};
		})
	);

	$effect(
		() =>
			(mutatedCopy = wordsArray.map((word) => {
				return {
					word: word,
					isMutated: false
				};
			}))
	);
	let interval = $state();

	const stop = () => {
		if (interval) {
			clearInterval(interval);
		}
	};

	const reset = () => {
		stop();
		mutatedCopy = wordsArray.map((word) => {
			return {
				word: word,
				isMutated: false
			};
		});
	};

	const mutateAlliteration = () => {
		stop();
		interval = setInterval(() => {
			let randIdx = Math.floor(Math.random() * mutatedCopy.length);
			let word = mutatedCopy[randIdx].word.replaceAll(/[.,!?]+/g, '');
			let pos = RiTa.pos(word, { simple: true })[0];
			let numSyllables = RiTa.syllables(word).split('/').length;
			let alliterations = RiTa.alliterationsSync(word, {
				shuffle: true,
				limit: 10,
				pos: pos,
				numSyllables: numSyllables
			});
			if (alliterations.length) {
				mutatedCopy[randIdx].word = alliterations[0];
				mutatedCopy[randIdx].isMutated = true;
			}
		}, 150);
	};

	const mutateSoundsLike = () => {
		stop();
		interval = setInterval(() => {
			let randIdx = Math.floor(Math.random() * mutatedCopy.length);
			let word = mutatedCopy[randIdx].word.replaceAll(/[.,!?]+/g, '');
			let pos = RiTa.pos(word, { simple: true })[0];
			let numSyllables = RiTa.syllables(word).split('/').length;
			let soundsLike = RiTa.soundsLikeSync(mutatedCopy[randIdx].word, {
				limit: 1,
				shuffle: true
			});
			if (soundsLike.length) {
				mutatedCopy[randIdx].word = soundsLike[0];
				mutatedCopy[randIdx].isMutated = true;
			}
		}, 250);
	};

	const mutateSpellsLike = () => {
		stop();
		interval = setInterval(() => {
			let randIdx = Math.floor(Math.random() * mutatedCopy.length);
			let word = mutatedCopy[randIdx].word.replaceAll(/[.,!?]+/g, '');
			let pos = RiTa.pos(word, { simple: true })[0];
			let numSyllables = RiTa.syllables(word).split('/').length;
			let spellsLike = RiTa.spellsLikeSync(mutatedCopy[randIdx].word, {
				limit: 1,
				shuffle: true
			});
			if (spellsLike.length) {
				mutatedCopy[randIdx].word = spellsLike[0];
				mutatedCopy[randIdx].isMutated = true;
			}
		}, 250);
	};

	const mutateRhyme = () => {
		stop();
		interval = setInterval(() => {
			let randIdx = Math.floor(Math.random() * mutatedCopy.length);
			let word = mutatedCopy[randIdx].word.replaceAll(/[.,!?]+/g, '');
			let pos = RiTa.pos(word, { simple: true })[0];
			let numSyllables = RiTa.syllables(word).split('/').length;
			let rhymes = RiTa.rhymesSync(mutatedCopy[randIdx].word, {
				limit: 1,
				shuffle: true
			});
			if (rhymes.length) {
				mutatedCopy[randIdx].word = rhymes[0];
				mutatedCopy[randIdx].isMutated = true;
			}
		}, 250);
	};
</script>

{#if siteState.text}
	<button onclick={reset} class="border p-4">Reset</button>

	<button onclick={stop} class="border p-4">Stop</button>
	<button onclick={mutateAlliteration} class="border p-4">Alliterations</button>
	<button onclick={mutateSoundsLike} class="border p-4">Sounds Like</button>
	<button onclick={mutateSpellsLike} class="border p-4">Spells Like</button>
	<button onclick={mutateRhyme} class="border p-4">Rhymes</button>

	<div class="flex justify-center">
		<div class="p-4 max-w-lg">
			{#each mutatedCopy as word, idx (idx)}
				<span class={word?.isMutated ? 'text-red-500' : ''}>
					{word?.word}{#if word?.isMutated}<span>({wordsArray[idx]})</span>{/if}
				</span>
				<span> </span>
			{/each}
		</div>
	</div>
{/if}
