<script lang="ts">
	import NavLink from '$lib/components/NavLink.svelte';
	import { siteState } from '$lib/states.svelte';
	let form: HTMLFormElement;
	let textarea: HTMLTextAreaElement;

	const onSubmit = (e: Event) => {
		e.preventDefault();
		siteState.text = textarea.value;
	};
</script>

<NavLink href={"/"}></NavLink>