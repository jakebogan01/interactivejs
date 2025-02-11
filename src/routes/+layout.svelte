<script>
	import '../app.css';
	import { global_data } from '$lib/stores/globalData.svelte.js';
	import Search from '$lib/components/Search.svelte';
	import Header from '$lib/components/Header.svelte';
	import Hero from '$lib/components/Hero.svelte';

	let { children } = $props();
</script>

{#if global_data.active === 'search'}
	<Search />
{/if}

<div class="flex w-full flex-col">
	<Header />

	<Hero />

	{@render children()}
</div>
