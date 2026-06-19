<script lang="ts">
	import Button from '$lib/components/Button.svelte';
	import { siteState } from '$lib/states.svelte';
	import { shuffle } from '$lib/utils';
	let initialWordsArray = $derived(
		siteState.text
			.trim()
			.replaceAll(/[.,!?]+/g, '')
			.split(' ')
	);

	let sortedWordsArray = $state(initialWordsArray);
	let lengthSortDirection = $state(true);

	const sortByLength = () => {
		sortedWordsArray = initialWordsArray;
		if (lengthSortDirection) {
			sortedWordsArray.sort((a, b) => {
				return a.length - b.length || a.localeCompare(b);
			});
		} else {
			sortedWordsArray.sort((a, b) => {
				return b.length - a.length || a.localeCompare(b);
			});
		}
		lengthSortDirection = !lengthSortDirection;
	};

	const sortAlphabetically = () => {
		sortedWordsArray = initialWordsArray;
		if (lengthSortDirection) {
			sortedWordsArray.sort((a, b) => {
				return a.localeCompare(b);
			});
		} else {
			sortedWordsArray.sort((a, b) => {
				return b.localeCompare(a);
			});
		}
		lengthSortDirection = !lengthSortDirection;
	};

	const randomShuffle = () => {
		shuffle(sortedWordsArray);
	};

	const reverseOrder = () => {
		sortedWordsArray = initialWordsArray.reverse();
	};
</script>

{#if siteState.text}
	<div class="p-4">
		<Button onclick={sortByLength}>Sort by length</Button>
		<Button onclick={sortAlphabetically}>Sort Alphabetically</Button>
		<Button onclick={randomShuffle}>Randomize</Button>
		<Button onclick={reverseOrder}>Reverse</Button>

		<div class="flex justify-center">
			<div class="p-4 max-w-lg">
				{#each sortedWordsArray as word, idx (idx)}
					<span>
						{word.toLowerCase()}
					</span>
					<span> </span>
				{/each}
			</div>
		</div>
	</div>
{/if}
