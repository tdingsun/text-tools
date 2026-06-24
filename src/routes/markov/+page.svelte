<script lang="ts">
	import Button from '$lib/components/Button.svelte';
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
	<div class="flex flex-col justify-center items-center">
		<Button onclick={generate} class="sticky top-8 bg-white">Generate</Button>

		<div class="flex justify-center">
			<div class="p-4 max-w-lg">
				{#each generatedSentences as sentences, i (i)}
					{#each sentences as sentence, j (j)}
						<div class="flex gap-4">
							<div>{i*3 + j + 1}</div>
							<div>
								{sentence}
							</div>
						</div>
					{/each}
				{/each}
			</div>
		</div>
	</div>
{/if}
