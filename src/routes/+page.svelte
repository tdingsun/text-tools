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
	<div class="flex flex-wrap gap-2 justify-center items-center">
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
	<div class="flex gap-2">
		<div>
			<NavLink
				target="_blank"
				href="https://docs.google.com/document/d/1190uTpfC6SvNqJJb7VSX8dNK-f8oCBHf-9g6YXc89JY/edit?usp=sharing"
				>Link to Readings</NavLink
			>
		</div>
		<div>
			<NavLink target="_blank" href="https://github.com/tdingsun/text-tools">Link to Github</NavLink
			>
		</div>
		<div>
			<NavLink target="_blank" href="https://drive.google.com/drive/folders/1f8RMZn6E43MbITkAkFgLIQvF9447Kr2r?usp=sharing">Link to Google Drive</NavLink
			>
		</div>
		
	</div>
</div>
