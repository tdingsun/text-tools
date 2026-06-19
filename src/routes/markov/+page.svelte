<script lang="ts">
	import { siteState } from '$lib/states.svelte';
	import { RiTa } from 'rita';
	import { onMount } from 'svelte';
	let rm = RiTa.markov(2);
	let generatedSentences: string[][] = $state([]);
	$effect(() => {
		rm = RiTa.markov(2);
		rm.addText(siteState.text);
	});

	onMount(() => {
		let rm = RiTa.markov(2);
		rm.addText(siteState.text);
	});

	const generate = () => {
		let sentences = rm.generate(3, {
			temperature: 2
		});
		generatedSentences.push(sentences);
	};
</script>

{#if siteState.text}
	<button onclick={generate} class="border p-4">Generate</button>

	<div class="flex justify-center">
		<div class="p-4 max-w-lg">
			{#each generatedSentences as sentences, idx (idx)}
				{#each sentences as sentence, idx (idx)}
					<div>
						{sentence}
					</div>
				{/each}
			{/each}
		</div>
	</div>
{/if}
