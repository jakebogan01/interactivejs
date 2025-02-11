<script>
	import { onMount } from 'svelte';
	import { scale, fade } from 'svelte/transition';
	import { global_search } from '$lib/stores/searchData.svelte.js';
	import hljs from 'highlight.js/lib/core';
	import 'highlight.js/styles/tomorrow-night-blue.css';
	import javascript from 'highlight.js/lib/languages/javascript';
	hljs.registerLanguage('javascript', javascript);

	let titleEl,
		currentIndex = $state(0),
		arrayLength = $state(null),
		blockColor = $state(null);

	onMount(() => {
		global_search.push({ id: titleEl.getAttribute('id'), title: titleEl.innerText });
	});

	let code = `let colors = [];

// Get index
colors.at();
// or
colors[];`;

	let createArray = $state(''),
		codeElement;
	createArray = hljs.highlight(code, { language: 'javascript' }).value;

	let array = $state([]);
	const colors = ['#f472b6', '#D163F9', '#0ea5e9', '#6963F9', '#F9F363', '#F98663'];

	const updateCode = () => {
		const colors = array.map((item) => {
			const obj = array.find((obj) => obj.id === item.id);
			return obj ? `"${obj.color}"` : '';
		});
		if (currentIndex > array.length - 1) {
			if (array.length !== 0) decrement();
		}
		code = `let colors = [${colors.join(', ')}];

// Get index at ${colors[currentIndex] ? currentIndex : ''}
colors.at(${colors[currentIndex] ? currentIndex : ''}); // ${colors[currentIndex] ? `${colors[currentIndex]}` : ''}
// or
colors[${colors[currentIndex] ? currentIndex : ''}]; // ${colors[currentIndex] ? `${colors[currentIndex]}` : ''}`;
		createArray = hljs.highlight(code, { language: 'javascript' }).value;
	};

	const addBlock = () => {
		let newNumber;
		do {
			newNumber = Math.floor(Math.random() * 6);
		} while (array.some((item) => item.id === newNumber));
		array = [...array, { id: newNumber, color: colors[array.length % colors.length] }];
		updateCode();
		arrayLength = array.length - 1;
	};

	const removeBlock = (id = null) => {
		if (array.length > 0) {
			if (id !== null) {
				array = array.filter((item) => item.id !== id);
			} else {
				array = array.slice(0, -1);
			}
			updateCode();
			arrayLength = array.length === 0 ? null : array.length - 1;
			if (currentIndex > arrayLength) currentIndex--;
			blockColor = array[currentIndex]?.color;
		}
	};

	const copyToClipboard = () => {
		if (codeElement) {
			const textToCopy = codeElement.innerText;
			navigator.clipboard
				.writeText(textToCopy)
				.then(() => {
					alert('Code copied to clipboard!');
				})
				.catch((err) => {
					console.error('Failed to copy code: ', err);
				});
		}
	};

	const increment = () => {
		if (currentIndex <= arrayLength - 1) currentIndex++;
		blockColor = array[currentIndex]?.color;
		updateCode();
	};

	const decrement = () => {
		if (currentIndex >= 1) currentIndex--;
		blockColor = array[currentIndex]?.color;
		updateCode();
	};
</script>

<h2 bind:this={titleEl} id="array-at" class="text-white">At()</h2>

<p>
	The <span class="text-sky-500">at()</span> method returns an indexed element from an array.
	<br />
	The <span class="text-sky-500">at()</span> method returns the same as
	<span class="text-sky-500">[ ]</span>.
	<br />
	The <span class="text-sky-500">at()</span> method is supported in all modern browsers since March 2022.
</p>

<div class="mb-[38px] flex">
	<h3 class="min-w-[75px] text-sm text-gray-400">Colors:</h3>
	<div class="flex">
		<div class="mr-2 flex flex-col justify-center space-y-3">
			<button
				type="button"
				onclick={addBlock}
				aria-label="add"
				class="cursor-pointer rounded-full border border-slate-700 bg-slate-800 text-gray-400 transition hover:bg-slate-600 hover:text-white disabled:border-slate-700 disabled:bg-slate-800 disabled:text-gray-400 disabled:opacity-50"
				disabled={array.length >= 6}
			>
				<svg
					xmlns="http://www.w3.org/2000/svg"
					viewBox="0 0 20 20"
					fill="currentColor"
					class="size-5"
					><path
						d="M10.75 4.75a.75.75 0 0 0-1.5 0v4.5h-4.5a.75.75 0 0 0 0 1.5h4.5v4.5a.75.75 0 0 0 1.5 0v-4.5h4.5a.75.75 0 0 0 0-1.5h-4.5v-4.5Z"
					/></svg
				>
			</button>
			<button
				type="button"
				onclick={() => removeBlock()}
				aria-label="remove"
				class="cursor-pointer rounded-full border border-slate-700 bg-slate-800 text-gray-400 transition hover:bg-slate-600 hover:text-white disabled:border-slate-700 disabled:bg-slate-800 disabled:text-gray-400 disabled:opacity-50"
				disabled={array.length === 0}
			>
				<svg
					xmlns="http://www.w3.org/2000/svg"
					viewBox="0 0 20 20"
					fill="currentColor"
					class="size-5"
					><path
						fill-rule="evenodd"
						d="M4 10a.75.75 0 0 1 .75-.75h10.5a.75.75 0 0 1 0 1.5H4.75A.75.75 0 0 1 4 10Z"
						clip-rule="evenodd"
					/></svg
				>
			</button>
		</div>
		<div class="relative">
			<div
				style="width: {array.length * 60 + 11.6}px;"
				class="flex min-h-[71.6px] min-w-[71.6px] space-x-2.5 overflow-hidden rounded-xl border border-slate-700 bg-slate-800 p-2.5 transition-[width] duration-300"
			>
				{#each array as item, index}
					<button
						transition:scale|local={{ duration: 500 }}
						type="button"
						aria-label="block"
						onclick={() => removeBlock(item.id)}
						class="group flex size-[50px] min-h-[50px] min-w-[50px] transform cursor-pointer items-center justify-center rounded-[5px] bg-pink-400 text-white transition duration-300 hover:scale-90 hover:!bg-red-500"
						style="background-color: {item.color};"
					>
						<svg
							xmlns="http://www.w3.org/2000/svg"
							viewBox="0 0 20 20"
							fill="currentColor"
							class="size-5 opacity-0 transition duration-300 group-hover:opacity-100"
							><path
								fill-rule="evenodd"
								d="M8.75 1A2.75 2.75 0 0 0 6 3.75v.443c-.795.077-1.584.176-2.365.298a.75.75 0 1 0 .23 1.482l.149-.022.841 10.518A2.75 2.75 0 0 0 7.596 19h4.807a2.75 2.75 0 0 0 2.742-2.53l.841-10.52.149.023a.75.75 0 0 0 .23-1.482A41.03 41.03 0 0 0 14 4.193V3.75A2.75 2.75 0 0 0 11.25 1h-2.5ZM10 4c.84 0 1.673.025 2.5.075V3.75c0-.69-.56-1.25-1.25-1.25h-2.5c-.69 0-1.25.56-1.25 1.25v.325C8.327 4.025 9.16 4 10 4ZM8.58 7.72a.75.75 0 0 0-1.5.06l.3 7.5a.75.75 0 1 0 1.5-.06l-.3-7.5Zm4.34.06a.75.75 0 1 0-1.5-.06l-.3 7.5a.75.75 0 1 0 1.5.06l.3-7.5Z"
								clip-rule="evenodd"
							/></svg
						>
					</button>
				{/each}
			</div>
			<div class="absolute flex min-w-[71.6px] space-x-2.5 overflow-hidden px-2.5">
				{#each array as item, index}
					<span
						transition:fade|local={{ duration: 150 }}
						aria-label="Block index"
						class="flex w-[50px] justify-center text-sm text-gray-400">{index}</span
					>
				{/each}
			</div>
		</div>
	</div>
</div>

<div class="flex min-h-[71.6px]">
	<h3 class="min-w-[75px] text-sm text-gray-400">Select:</h3>
	<div class="flex">
		<div class="mr-2 flex flex-col justify-center space-y-3">
			<button
				type="button"
				onclick={increment}
				aria-label="add"
				class="cursor-pointer rounded-full border border-slate-700 bg-slate-800 text-gray-400 transition hover:bg-slate-600 hover:text-white disabled:border-slate-700 disabled:bg-slate-800 disabled:text-gray-400 disabled:opacity-50"
				disabled={currentIndex >= 5 || array.length === 0}
			>
				<svg
					xmlns="http://www.w3.org/2000/svg"
					viewBox="0 0 20 20"
					fill="currentColor"
					class="size-5"
					><path
						d="M10.75 4.75a.75.75 0 0 0-1.5 0v4.5h-4.5a.75.75 0 0 0 0 1.5h4.5v4.5a.75.75 0 0 0 1.5 0v-4.5h4.5a.75.75 0 0 0 0-1.5h-4.5v-4.5Z"
					/></svg
				>
			</button>
			<button
				type="button"
				onclick={decrement}
				aria-label="remove"
				class="cursor-pointer rounded-full border border-slate-700 bg-slate-800 text-gray-400 transition hover:bg-slate-600 hover:text-white disabled:border-slate-700 disabled:bg-slate-800 disabled:text-gray-400 disabled:opacity-50"
				disabled={array.length <= 1}
			>
				<svg
					xmlns="http://www.w3.org/2000/svg"
					viewBox="0 0 20 20"
					fill="currentColor"
					class="size-5"
					><path
						fill-rule="evenodd"
						d="M4 10a.75.75 0 0 1 .75-.75h10.5a.75.75 0 0 1 0 1.5H4.75A.75.75 0 0 1 4 10Z"
						clip-rule="evenodd"
					/></svg
				>
			</button>
		</div>
		{#if arrayLength !== null}
			<div
				transition:scale|local={{ duration: 500 }}
				class="flex min-h-[71.6px] max-w-[105px] min-w-[105px] space-x-2.5 overflow-hidden rounded-xl border border-slate-700 bg-slate-800 p-2.5"
			>
				<span class="flex max-w-[23.4px] min-w-[23.4px] flex-1 items-center justify-center text-xl"
					>{currentIndex}</span
				>
				<div
					class="size-[50px] min-h-[50px] min-w-[50px] rounded-[5px]"
					style="background-color: {blockColor ? blockColor : array[currentIndex]?.color};"
				></div>
			</div>
		{/if}
	</div>
</div>

<div class="my-6 flex">
	<h3 class="min-w-[75px] text-sm text-gray-400">Code:</h3>
	<div class="group relative flex-1">
		<button
			onclick={copyToClipboard}
			type="button"
			aria-label="Copy code"
			title="Copy code"
			class="absolute top-1.5 right-1.5 cursor-pointer text-slate-600 opacity-0 transition group-hover:opacity-100 hover:text-slate-400"
		>
			<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="size-6"
				><path
					d="M7.5 3.375c0-1.036.84-1.875 1.875-1.875h.375a3.75 3.75 0 0 1 3.75 3.75v1.875C13.5 8.161 14.34 9 15.375 9h1.875A3.75 3.75 0 0 1 21 12.75v3.375C21 17.16 20.16 18 19.125 18h-9.75A1.875 1.875 0 0 1 7.5 16.125V3.375Z"
				/><path
					d="M15 5.25a5.23 5.23 0 0 0-1.279-3.434 9.768 9.768 0 0 1 6.963 6.963A5.23 5.23 0 0 0 17.25 7.5h-1.875A.375.375 0 0 1 15 7.125V5.25ZM4.875 6H6v10.125A3.375 3.375 0 0 0 9.375 19.5H16.5v1.125c0 1.035-.84 1.875-1.875 1.875h-9.75A1.875 1.875 0 0 1 3 20.625V7.875C3 6.839 3.84 6 4.875 6Z"
				/></svg
			>
		</button>
		<pre class="!m-0 flex overflow-x-auto pb-6"><code
				bind:this={codeElement}
				class="hljs language-javascript !bg-transparent !p-0">{@html createArray}</code
			></pre>
	</div>
</div>
