<script lang="ts">
	let { onclick = null, children, class: className = '' } = $props();
</script>

<button {onclick} class="border px-2 py-1 rounded hover:bg-green-100 cursor-pointer {className}">
	{@render children()}
</button>
