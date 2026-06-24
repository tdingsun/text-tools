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

<svelte:head>
<title>Text Tools</title>
</svelte:head>

{#if page.url.pathname !== '/'}
	<div class="flex w-full gap-4 p-4 border-b">
		<a href="/" class="whitespace-nowrap pt-1">Text Tools</a>

		<div>
			<div class="flex gap-1 flex-wrap">
				<NavLink href="/reader">1. Reader</NavLink>
				<NavLink href="/grid">2. Grid</NavLink>
				<NavLink href="/sort">3. Sort</NavLink>
				<NavLink href="/frequency">4. Frequency</NavLink>
				<NavLink href="/blur">5. Blur</NavLink>
				<NavLink href="/jitter">6. Jitter</NavLink>
				<NavLink href="/cloud">7. Cloud</NavLink>
				<NavLink href="/mutation">8. Mutation</NavLink>
				<NavLink href="/generation">9. Generation</NavLink>
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
