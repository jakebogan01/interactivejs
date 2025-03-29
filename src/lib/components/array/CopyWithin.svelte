<script>
	import { onMount } from 'svelte';
	import { scale, fade } from 'svelte/transition';
	import { global_search } from '$lib/stores/searchData.svelte.js';
	import hljs from 'highlight.js/lib/core';
	import 'highlight.js/styles/tomorrow-night-blue.css';
	import javascript from 'highlight.js/lib/languages/javascript';
	hljs.registerLanguage('javascript', javascript);

	let titleEl, tureky;

	onMount(() => {
		global_search.push({ id: titleEl.getAttribute('id'), title: titleEl.innerText });
	});

	let code = `// Copy to index 2, all colors from index 0
const colors = [];
const results = colors.copyWithin(2, 0);
// `;

	let createArray = $state(''),
		codeElement;
	createArray = hljs.highlight(code, { language: 'javascript' }).value;

	let array1 = $state([]),
		array2 = $state([]),
		array3 = $state([]);

	const colors1 = ['#f472b6', '#D163F9', '#0ea5e9'];
	const colors2 = ['#6963F9', '#F9F363', '#F98663'];

	const updateCode = () => {
		const colors1 = array1.map((item) => {
			const obj = array1.find((obj) => obj.id === item.id);
			return obj ? `"${obj.color}"` : '';
		});
		const colors2 = array2.map((item) => {
			const obj = array2.find((obj) => obj.id === item.id);
			return obj ? `"${obj.color}"` : '';
		});
		const test = colors1.concat(colors2);
		const children = test.map((item) => `${item}`);
		code = `// Copy to index 2, all colors from index 0
const colors = [${colors1.join(', ')}];
const results = colors1.concat(colors2);
// ${children.join(', ')}`;
		createArray = hljs.highlight(code, { language: 'javascript' }).value;
	};

	const addBlock = (num, array) => {
		let newNumber;
		do {
			newNumber = Math.floor(Math.random() * 3);
		} while (array.some((item) => item.id === newNumber));
		if (num === 1) array.push({ id: newNumber, color: colors1[array.length % colors1.length] });
		if (num === 2) array.push({ id: newNumber, color: colors2[array.length % colors2.length] });
		updateCode();
		joinArrays();
	};

	const removeBlock = (array, id = null) => {
		if (array.length > 0) {
			if (id !== null) {
				const index = array.findIndex((item) => item.id === id);
				if (index !== -1) array.splice(index, 1);
			} else {
				array.pop();
			}
			updateCode();
			joinArrays();
		}
	};

	const joinArrays = () => (array3 = array1.concat(array2));

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
</script>

<h2 bind:this={titleEl} id="array-copywithin" class="text-white">CopyWithin()</h2>

<p>
	The <span class="text-sky-500">copyWithin()</span> method copies array elements to another position in an array.
	<br />
	The <span class="text-sky-500">copyWithin()</span> method overwrites the existing values.
	<br />
	The <span class="text-sky-500">copyWithin()</span> method does not add items to the array.
</p>

<div class="mb-[38px] flex">
	<h3 class="min-w-[75px] text-sm text-gray-400">Colors:</h3>
	<div class="flex">
		<div class="mr-2 flex flex-col justify-center space-y-3">
			<button
				type="button"
				onclick={() => addBlock(1, array1)}
				aria-label="add"
				class="cursor-pointer rounded-full border border-slate-700 bg-slate-800 text-gray-400 transition hover:bg-slate-600 hover:text-white disabled:border-slate-700 disabled:bg-slate-800 disabled:text-gray-400 disabled:opacity-50"
				disabled={array1.length >= 3}
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
				onclick={() => removeBlock(array1)}
				aria-label="remove"
				class="cursor-pointer rounded-full border border-slate-700 bg-slate-800 text-gray-400 transition hover:bg-slate-600 hover:text-white disabled:border-slate-700 disabled:bg-slate-800 disabled:text-gray-400 disabled:opacity-50"
				disabled={array1.length === 0}
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
			<span bind:this={tureky} class="block absolute top-0 bg-red-500 size-10"></span>
			<div
				style="width: {array1.length * 60 + 11.6}px;"
				class="flex min-h-[71.6px] min-w-[71.6px] space-x-2.5 overflow-hidden rounded-xl border border-slate-700 bg-slate-800 p-2.5 transition-[width] duration-300"
			>
				{#each array1 as item, index}
					<button
						transition:scale|local={{ duration: 500 }}
						onmouseenter={(e)=>{console.log(tureky.style.transform = `translateX(${e.clientX}px)`)}}
						type="button"
						aria-label="block"
						class="group flex size-[50px] min-h-[50px] min-w-[50px] transform cursor-pointer items-center justify-center rounded-[5px] bg-pink-400 text-white transition duration-300 hover:scale-90"
						style="background-color: {item.color};"
					>
						<svg
							xmlns="http://www.w3.org/2000/svg"
							viewBox="0 0 24 24"
							fill="currentColor"
							class="size-5 opacity-0 transition duration-300 group-hover:opacity-100"
							><path
								fill-rule="evenodd"
							  	d="M4.5 5.653c0-1.427 1.529-2.33 2.779-1.643l11.54 6.347c1.295.712 1.295 2.573 0 3.286L7.28 19.99c-1.25.687-2.779-.217-2.779-1.643V5.653Z"
								clip-rule="evenodd"
							/></svg
						>
					</button>
				{/each}
			</div>
			<div class="absolute flex min-w-[71.6px] space-x-2.5 overflow-hidden px-2.5">
				{#each array1 as item, index}
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

<div class="mb-[38px] flex min-h-[71.6px]">
	<h3 class="min-w-[75px] text-sm text-gray-400">Results:</h3>
	{#if array3.length > 0}
		<div class="relative">
			<div
				transition:scale|local={{ duration: 500 }}
				style="width: {array3.length * 60 + 11.6}px;"
				class="flex min-h-[71.6px] min-w-[71.6px] space-x-2.5 overflow-hidden rounded-xl border border-slate-700 bg-slate-800 p-2.5 transition-[width] duration-300"
			>
				{#each array3 as item, index}
					<div
						transition:scale|local={{ duration: 500 }}
						class="size-[50px] min-h-[50px] min-w-[50px] rounded-[5px]"
						style="background-color: {item.color};"
					></div>
				{/each}
			</div>
			<div
				transition:fade|local={{ duration: 150 }}
				class="absolute flex min-w-[71.6px] space-x-2.5 overflow-hidden px-2.5"
			>
				{#each array3 as item, index}
					<span
						transition:fade|local={{ duration: 150 }}
						aria-label="Block index"
						class="flex w-[50px] justify-center text-sm text-gray-400">{index}</span
					>
				{/each}
			</div>
		</div>
	{/if}
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
