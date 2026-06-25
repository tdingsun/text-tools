<script lang="ts">
	import Button from '$lib/components/Button.svelte';
	import { siteState } from '$lib/states.svelte';
	import { RiTa } from 'rita';
	import { onMount } from 'svelte';
	let rm = RiTa.markov(2);
	let generatedSentences: string[][] = $state([]);
	let temp = $state(2);
	let numTokens = $state(2);
	let numSentences = $state(1);
	$effect(() => {
		rm = RiTa.markov(numTokens);
		rm.addText(siteState.text);
	});

	onMount(() => {
		let rm = RiTa.markov(numTokens);
		rm.addText(siteState.text);
	});

	const generate = () => {
		let sentences;
		if (numSentences === 1) {
			sentences = [
				rm.generate({
					temperature: temp
				})
			];
		} else {
			sentences = rm.generate(numSentences, {
				temperature: temp
			});
		}

		generatedSentences.push(sentences);
	};
</script>

{#if siteState.text}
	<div class="flex gap-4 justify-center mb-4">
		<span>Temperature</span><input type="range" min="1" max="10" bind:value={temp} /><span
			>{temp}</span
		>
		<span># Sentences</span><input type="range" min="1" max="10" bind:value={numSentences} /><span
			>{numSentences}</span
		>
	</div>
	<div class="flex flex-col justify-center items-center">
		<Button onclick={generate} class="sticky top-8 bg-white">Generate</Button>

		<div class="flex justify-center">
			<div class="p-4 max-w-lg flex flex-col-reverse gap-4">
				{#each generatedSentences as sentences, i (i)}
					<div class="flex gap-4">
						<div class="text-xs pt-1">{i + 1}</div>
						<div>
							{#each sentences as sentence, j (j)}
								{sentence + ' '}
							{/each}
						</div>
					</div>
				{/each}
			</div>
		</div>
	</div>
{/if}
