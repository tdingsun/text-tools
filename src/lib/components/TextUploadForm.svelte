<script lang="ts">
	import { siteState } from '$lib/states.svelte';
	let textarea: HTMLTextAreaElement;

	const onSubmit = (e: Event) => {
		e.preventDefault();
		siteState.text = textarea.value;
		localStorage.setItem('text', textarea.value);
		textarea.value = '';
	};
</script>

<form onsubmit={onSubmit} class="flex items-center w-full h-12">
	<textarea
		bind:this={textarea}
		maxlength="9999"
		class=" w-full border border-r-0 rounded-l text-xs h-full resize-none"
		id="text"></textarea>
		<button
			type="submit"
			class="px-4 rounded-r h-full border whitespace-nowrap cursor-pointer hover:bg-black hover:text-white"
		>
			Upload Text
		</button>
</form>
