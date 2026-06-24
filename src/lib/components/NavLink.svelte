<script lang="ts">
import { page } from "$app/state";
	let { href, children, target = "_top" } = $props();
</script>

<a {href} {target} class="border px-2 py-1 rounded hover:bg-green-50 {page.url.pathname === href ? 'bg-green-200' : ''} cursor-pointer">
	{@render children?.()}
</a>
