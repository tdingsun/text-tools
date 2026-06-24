<script lang="ts">
	import Button from '$lib/components/Button.svelte';
	import { siteState } from '$lib/states.svelte';
	import { shuffle } from '$lib/utils';
	let initialWordsArray = $derived(
		siteState.text
			.trim()
			// .replaceAll(/[.,!?]+/g, '')
			.split(' ')
	);

	let sortedWordsArray = $state(initialWordsArray);
	let lengthSortDirection = $state(true);
	let alphaSortDirection = $state(true);
	let orderSortDirection = $state(true);

	const sortByLength = () => {
		sortedWordsArray = initialWordsArray;
		if (lengthSortDirection) {
			sortedWordsArray.sort((a, b) => {
				return (
					a.replaceAll(/[.,!?]+/g, '').length - b.replaceAll(/[.,!?]+/g, '').length ||
					a.localeCompare(b)
				);
			});
		} else {
			sortedWordsArray.sort((a, b) => {
				return (
					b.replaceAll(/[.,!?]+/g, '').length - a.replaceAll(/[.,!?]+/g, '').length ||
					a.localeCompare(b)
				);
			});
		}
		lengthSortDirection = !lengthSortDirection;
	};

	const sortAlphabetically = () => {
		sortedWordsArray = initialWordsArray;
		if (alphaSortDirection) {
			sortedWordsArray.sort((a, b) => {
				return a.localeCompare(b);
			});
		} else {
			sortedWordsArray.sort((a, b) => {
				return b.localeCompare(a);
			});
		}
		alphaSortDirection = !alphaSortDirection;
	};

	const randomShuffle = () => {
		shuffle(sortedWordsArray);
	};

	const reverseOrder = () => {
		sortedWordsArray = initialWordsArray.reverse();
		orderSortDirection = !orderSortDirection;
	};
</script>

{#if siteState.text}
	<div class="flex flex-col justify-center items-center gap-8">
		<div>
			<Button onclick={reverseOrder}
				>{orderSortDirection ? 'Reverse Order' : 'Original Order'}</Button
			>

			<Button onclick={sortByLength}
				>Sort by Length <span>{lengthSortDirection ? '↑' : '↓'}</span></Button
			>
			<Button onclick={sortAlphabetically}
				>Sort Alphabetically <span>{alphaSortDirection ? '↑' : '↓'}</span></Button
			>
			<Button onclick={randomShuffle}>Randomize <span></span></Button>
		</div>

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
