<script lang="ts">
	import JitterChar from './JitterChar.svelte';
	import { siteState } from '$lib/states.svelte';
	import Button from '$lib/components/Button.svelte';
	let wordArray = $derived(siteState.text.trim().split(' '));
	let charArray = $derived(siteState.text.trim().split(''));
	let speed = $state(1);
	let useLetters = $state(false);
</script>

{#if siteState.text}
	<div class="flex gap-4 justify-center mb-8">
		<span>Speed</span>
		<input type="range" min="1" max="10" bind:value={speed} />
		<Button onclick={() => useLetters = !useLetters}>{useLetters ? 'Use Words' : 'Use Letters'}</Button>
	</div>
	<div class="flex flex-wrap p-4 justify-center items-center">
		<div class="max-w-lg">
		{#if useLetters}
			{#each charArray as char, idx (idx)}
				<JitterChar {char} {speed}></JitterChar>
			{/each}
			{:else}
			{#each wordArray as word, idx (idx)}
				<JitterChar char={word + '&nbsp;'} {speed}></JitterChar>
			{/each}
			{/if}
		</div>
	</div>
{/if}
