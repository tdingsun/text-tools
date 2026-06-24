<script lang="ts">
	import Button from '$lib/components/Button.svelte';
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

	let mode = $state('');

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
		mode = '';
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
		mode = 'alliteration';

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
		mode = 'soundslike';

		interval = setInterval(() => {
			let randIdx = Math.floor(Math.random() * mutatedCopy.length);
			let word = mutatedCopy[randIdx].word.replaceAll(/[.,!?]+/g, '');
			let soundsLike = RiTa.soundsLikeSync(word, {
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
		mode = 'spellslike';

		interval = setInterval(() => {
			let randIdx = Math.floor(Math.random() * mutatedCopy.length);
			let word = mutatedCopy[randIdx].word.replaceAll(/[.,!?]+/g, '');
			let spellsLike = RiTa.spellsLikeSync(word, {
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
		mode = 'rhyme';

		interval = setInterval(() => {
			let randIdx = Math.floor(Math.random() * mutatedCopy.length);
			let word = mutatedCopy[randIdx].word.replaceAll(/[.,!?]+/g, '');
			let rhymes = RiTa.rhymesSync(word, {
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

<div class="flex flex-col gap-8 justify-center items-center">
	<div class="flex gap-8">
		<div>
			<Button onclick={mutateAlliteration} class="{mode === 'alliteration' ? 'bg-green-100' : ''}">Alliterations</Button>
			<Button onclick={mutateSoundsLike} class="{mode === 'soundslike' ? 'bg-green-100' : ''}">Sounds Like</Button>
			<Button onclick={mutateSpellsLike} class="{mode === 'spellslike' ? 'bg-green-100' : ''}">Spells Like</Button>
			<Button onclick={mutateRhyme} class="{mode === 'rhyme' ? 'bg-green-100' : ''}">Rhymes</Button>
		</div>
		<div>
			<Button onclick={reset}>Reset</Button>

			<Button onclick={stop}>Stop</Button>
		</div>
	</div>

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
</div>
