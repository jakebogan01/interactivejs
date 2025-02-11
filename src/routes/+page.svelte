<script>
	import { global_data } from '$lib/stores/globalData.svelte.js';
	import Head from '$lib/components/Head.svelte';
	import SideNav from '$lib/components/SideNav.svelte';
	import Create from '$lib/components/array/Create.svelte';
	import At from '$lib/components/array/At.svelte';
	import Concat from '$lib/components/array/Concat.svelte';

	$inspect(global_data.active);
</script>

<Head
	page_title="Home"
	description="Master JavaScript array methods through interactive visuals and hands-on examples. Explore detailed descriptions, dynamic data flow visualizations, and practical code snippets to boost your coding skills."
	keywords="InteractiveJS, JavaScript, array methods, learn JavaScript, visual learning, interactive coding, JavaScript tutorials, code snippets, data flow visualization, JavaScript arrays"
/>

<main
	id="getting-started"
	class="max-w-8xl relative mx-auto flex w-full flex-auto justify-center sm:px-2 lg:px-8 xl:px-12"
>
	<div class="max-w-2xl min-w-0 flex-auto px-4 py-16 lg:max-w-none lg:pr-0 lg:pl-0 xl:pr-16">
		<article>
			<header class="mb-9 space-y-1">
				<p class="font-display text-sm font-medium text-sky-500">Introduction</p>
				<h1 class="font-display text-3xl tracking-tight text-white">JavaScript array methods</h1>
			</header>
			<div
				class="prose prose-slate prose-invert prose-headings:scroll-mt-28 prose-headings:font-display prose-headings:font-normal lg:prose-headings:scroll-mt-[8.5rem] prose-lead:text-slate-400 prose-a:text-sky-400 prose-a:no-underline prose-a:shadow-[inset_0_calc(-1*var(--tw-prose-underline-size,2px))_0_0_var(--tw-prose-underline,var(--color-sky-800))] prose-a:hover:[--tw-prose-underline-size:6px] prose-pre:rounded-xl prose-pre:bg-slate-800/60 prose-pre:ring-1 prose-pre:shadow-none prose-pre:ring-slate-300/10 prose-hr:border-slate-800 max-w-none text-slate-400 [--tw-prose-background:var(--color-slate-900)]"
			>
				<p class="lead">Learn JavaScript array methods in a new interactive experience.</p>
				<p>
					Explore detailed descriptions, dynamic data flow visualizations, and practical code
					snippets to boost your JavaScript array skills.
				</p>
				<hr />

				<Create />

				<hr />

				<At />

				<hr />

				<Concat />
			</div>
		</article>
	</div>

	<SideNav />
</main>
