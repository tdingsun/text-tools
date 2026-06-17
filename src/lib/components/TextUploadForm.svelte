<script lang="ts">
	import { siteState } from '$lib/states.svelte';
	let textarea: HTMLTextAreaElement;

	const onSubmit = (e: Event) => {
		e.preventDefault();
		siteState.text = textarea.value;
	};
</script>

<div class="flex flex-col gap-4 max-w-lg">
	<form onsubmit={onSubmit} class="flex flex-col">
		<textarea bind:this={textarea} class="border text-xs field-sizing-content min-h-12" id="text"
		></textarea>
		<div>
			<button
				type="submit"
				class="px-4 py-3 border border-t-0 cursor-pointer hover:bg-black hover:text-white"
			>
				Upload Text
			</button>
		</div>
	</form>
</div>
