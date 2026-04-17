<script lang="ts">
	import './layout.css';
	import favicon from '$lib/assets/images/favicon.png';
	import '$lib/styles/global.css';
	import '$lib/assets/fonts/Inter-VF.woff2';
	import '$lib/assets/fonts/JetBrainsMono-VF.woff2';

	let { children } = $props();
</script>

<svelte:head><link rel="icon" href={favicon} /></svelte:head>
<main class="pt-4">
{@render children()}
</main>