<script lang="ts">
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
    }

    const reverseOrder = () => {
        sortedWordsArray = initialWordsArray.reverse();
    }
</script>

{#if siteState.text}
	<button onclick={sortByLength} class="border">Sort by length</button>
	<button onclick={sortAlphabetically} class="border">Sort Alphabetically</button>
	<button onclick={randomShuffle} class="border">Randomize</button>
    	<button onclick={reverseOrder} class="border">Reverse</button>

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
{/if}
