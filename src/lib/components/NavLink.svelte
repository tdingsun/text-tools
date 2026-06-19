<script lang="ts">
	let { href, children } = $props();
</script>

<a {href} class="border px-2 py-1 rounded hover:bg-green-50 cursor-pointer">
	{@render children?.()}
</a>
