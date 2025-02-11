<script>
	import { onMount } from 'svelte';
	import { global_search } from '$lib/stores/searchData.svelte.js';

	let activeSection = $state(null);

	onMount(() => {
		const sections = document.querySelectorAll('h2');
		const observerOptions = {
			root: null,
			rootMargin: '0px',
			threshold: 0.5
		};

		const observer = new IntersectionObserver((entries) => {
			entries.forEach((entry) => {
				if (entry.isIntersecting) activeSection = entry.target.id;
			});
		}, observerOptions);

		sections.forEach((section) => {
			observer.observe(section);
		});

		return () => {
			sections.forEach((section) => {
				observer.unobserve(section);
			});
		};
	});
</script>

<div
	class="hidden xl:sticky xl:top-[4.75rem] xl:-mr-6 xl:block xl:h-[calc(100vh-4.75rem)] xl:flex-none xl:overflow-y-auto xl:py-16 xl:pr-6"
>
	<nav aria-labelledby="on-this-page-title" class="w-56">
		<h3 id="on-this-page-title" class="font-display text-sm font-medium text-white">
			On this page
		</h3>
		<ol role="list" class="mt-4 space-y-3 text-sm">
			{#each global_search as item}
				<li>
					<h4>
						<a
							class="font-normal text-slate-400 hover:text-slate-300 {activeSection === item.id
								? '!text-sky-500'
								: ''} transition-colors"
							href="#{item.id}">{item.title}</a
						>
					</h4>
				</li>
			{/each}
		</ol>
	</nav>
</div>
