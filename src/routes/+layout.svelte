<script>
	import '../app.css';
	import { injectAnalytics } from '@vercel/analytics/sveltekit';
	import { injectSpeedInsights } from '@vercel/speed-insights/sveltekit';
	import { global_data } from '$lib/stores/globalData.svelte.js';
	import Search from '$lib/components/Search.svelte';
	import Header from '$lib/components/Header.svelte';
	import Hero from '$lib/components/Hero.svelte';
	injectAnalytics();
	injectSpeedInsights();

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
