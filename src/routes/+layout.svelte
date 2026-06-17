<script lang="ts">
	import './layout.css';
	import favicon from '$lib/assets/favicon.svg';
	import CurrentTextDisplay from '$lib/components/CurrentTextDisplay.svelte';
	import TextUploadForm from '$lib/components/TextUploadForm.svelte';

	let { children } = $props();
</script>

<svelte:head><link rel="icon" href={favicon} /></svelte:head>

<div class="flex w-full gap-4 p-4 border-b">
	<div class="basis-1/2">
		<TextUploadForm></TextUploadForm>
	</div>
	<div class="basis-1/2">
		<CurrentTextDisplay></CurrentTextDisplay>
	</div>
</div>

<div class="">
	{@render children()}
</div>
