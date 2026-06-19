<script lang="ts">
	import CurrentTextDisplay from '$lib/components/CurrentTextDisplay.svelte';
	import NavLink from '$lib/components/NavLink.svelte';
	import TextUploadForm from '$lib/components/TextUploadForm.svelte';
</script>

<div class="flex flex-col justify-center items-center min-h-dvh w-full gap-4 p-4 border-b">
	<div class="w-full max-w-lg">
		<TextUploadForm></TextUploadForm>
	</div>
	<CurrentTextDisplay></CurrentTextDisplay>
	<div class="flex">
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
