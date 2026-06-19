<script lang="ts">
	import './layout.css';
	import favicon from '$lib/assets/favicon.svg';
	import TextUploadForm from '$lib/components/TextUploadForm.svelte';
	import NavLink from '$lib/components/NavLink.svelte';
	import { page } from '$app/state';
	import { onMount } from 'svelte';
	import { siteState } from '$lib/states.svelte';
	let { children } = $props();
	onMount(() => {
		let storedText = localStorage.getItem('text');
		if (storedText) {
			siteState.text = storedText;
		}
	});
</script>

<svelte:head><link rel="icon" href={favicon} /></svelte:head>

{#if page.url.pathname !== '/'}
	<div class="flex w-full gap-4 p-4 border-b">
		<div>TextTools</div>

		<div>
			<div class="flex gap-2 flex-wrap">
				<NavLink href="/sort">Sort</NavLink>
				<NavLink href="/reader">Reader</NavLink>
				<NavLink href="/mutation">Mutation</NavLink>
				<NavLink href="/markov">Markov</NavLink>
				<NavLink href="/jitter">Jitter</NavLink>
				<NavLink href="/grid">Grid</NavLink>
				<NavLink href="/frequency">Frequency</NavLink>
				<NavLink href="/cloud">Cloud</NavLink>
				<NavLink href="/blur">Blur</NavLink>
			</div>
		</div>
		<div class="basis-1/2">
			<TextUploadForm></TextUploadForm>
		</div>
	</div>
{/if}

{#if siteState.text || page.url.pathname === '/'}
	<div class="p-4">
		{@render children()}
	</div>
{/if}
