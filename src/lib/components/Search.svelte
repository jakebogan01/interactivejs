<script>
	import { fade, scale } from 'svelte/transition';
	import { quadIn } from 'svelte/easing';
	import { global_data } from '$lib/stores/globalData.svelte.js';
	import { global_search } from '$lib/stores/searchData.svelte.js';

	let searchInput = $state(),
		searchQuery = $state('');

	$effect(() => {
		if (searchInput) searchInput.focus();
	});

	const keyActions = (event) => {
		if (event.key === 'Escape') global_data.active = null;
	};

	const filteredResults = $derived.by(() => {
		if (!searchQuery) return [];
		return global_search.filter((item) => {
			const title = item.title || '';
			return title.toLowerCase().includes(searchQuery.toLowerCase());
		});
	});

	const closeSearchModal = (event) => {
		if (!event.target.closest('.search-modal')) global_data.active = null;
	};
</script>

<div
	class="fixed inset-0 z-100"
	onclick={closeSearchModal}
	onkeydown={closeSearchModal}
	role="tab"
	tabindex="-1"
	aria-label="Open tab"
	aria-labelledby="open-search-modal"
>
	<div class="fixed inset-0 bg-slate-900/50 backdrop-blur-sm"></div>
	<div
		transition:fade|local={{ duration: 300 }}
		class="fixed inset-0 overflow-y-auto px-4 py-4 sm:px-6 sm:py-20 md:py-32 lg:px-8 lg:py-[15vh]"
	>
		<div
			transition:scale|local={{ start: 0.95, opacity: 0, duration: 100, easing: quadIn }}
			role="tab"
			tabindex="-1"
			aria-label="Open tab"
			class="search-modal mx-auto transform-gpu overflow-hidden rounded-xl bg-slate-800 ring-1 shadow-xl ring-slate-700 sm:max-w-xl"
		>
			<div aria-expanded="false" aria-haspopup="listbox">
				<form action="" novalidate="" role="search">
					<div class="group relative flex h-12">
						<svg
							aria-hidden="true"
							viewBox="0 0 20 20"
							class="pointer-events-none absolute top-0 left-4 h-full w-5 fill-slate-500"
							><path
								d="M16.293 17.707a1 1 0 0 0 1.414-1.414l-1.414 1.414ZM9 14a5 5 0 0 1-5-5H2a7 7 0 0 0 7 7v-2ZM4 9a5 5 0 0 1 5-5V2a7 7 0 0 0-7 7h2Zm5-5a5 5 0 0 1 5 5h2a7 7 0 0 0-7-7v2Zm8.707 12.293-3.757-3.757-1.414 1.414 3.757 3.757 1.414-1.414ZM14 9a4.98 4.98 0 0 1-1.464 3.536l1.414 1.414A6.98 6.98 0 0 0 16 9h-2Zm-1.464 3.536A4.98 4.98 0 0 1 9 14v2a6.98 6.98 0 0 0 4.95-2.05l-1.414-1.414Z"
							></path></svg
						>
						<input
							bind:this={searchInput}
							bind:value={searchQuery}
							onkeydown={keyActions}
							data-autofocus="true"
							class="flex-auto appearance-none bg-transparent pr-4 pl-12 text-white outline-hidden placeholder:text-slate-400 focus:w-full focus:flex-none sm:text-sm"
							aria-autocomplete="both"
							autocomplete="off"
							autocorrect="off"
							autocapitalize="off"
							enterkeyhint="go"
							spellcheck="false"
							placeholder="Find something..."
							maxlength="512"
							type="text"
						/>
					</div>
					{#if searchQuery}
						<div class="border-t border-slate-400/10 bg-slate-800 px-2 py-3 empty:hidden">
							<ul role="listbox">
								{#each filteredResults as item}
									<li
										class="group block cursor-default rounded-lg hover:aria-selected:bg-slate-700/30"
										tabindex="-1"
										role="option"
										aria-selected="true"
									>
										<a
											href="#{item.id}"
											onclick={() => (global_data.active = null)}
											aria-hidden="true"
											class="block px-3 py-2 text-sm text-slate-300 hover:group-aria-selected:text-sky-400"
										>
											{item.title}
										</a>
									</li>
								{/each}
							</ul>
						</div>
					{/if}
				</form>
			</div>
		</div>
	</div>
</div>
