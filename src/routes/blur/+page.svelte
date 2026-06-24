<script lang="ts">
	import Button from '$lib/components/Button.svelte';
	import { siteState } from '$lib/states.svelte';
	let wordsArray = $derived(
		siteState.text
			.trim()
			.replaceAll(/[.,!?]+/g, '')
			.split(' ')
	);
	let numButtons = new Array(10);
	let mod = $state(1);
	let displayType = $state('blur');
</script>

{#if siteState.text}
	<div class="p-4">
		<div class="flex gap-8 justify-center pb-8">
			<div class="flex gap-1">
				{#each numButtons as _, idx (idx)}
					<Button onclick={() => (mod = idx + 1)} class="{mod === idx + 1 ? 'bg-green-200' : ''}">{idx + 1}</Button>
				{/each}
			</div>
			<div>
				<Button
					onclick={() => (displayType = 'blur')}
					class={displayType === 'blur' ? 'bg-green-100' : ''}>Blur</Button
				>
				<Button
					onclick={() => (displayType = 'vanish')}
					class={displayType === 'vanish' ? 'bg-green-100' : ''}>Vanish</Button
				>
			</div>
		</div>

		<div class="flex justify-center">
			<div class="p-4 max-w-lg">
				{#each wordsArray as word, idx (idx)}
					<span
						class="{idx % mod === 0
							? 'blur-[0px]'
							: displayType === 'blur'
								? 'blur-xs opacity-100'
								: ' blur-xs opacity-0'} transition-[opacity,filter] duration-250 transform-3d"
					>
						{word.toLowerCase()}
					</span>
					<span> </span>
				{/each}
			</div>
		</div>
	</div>
{/if}
