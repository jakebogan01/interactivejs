<script>
	import { global_search } from '$lib/stores/searchData.svelte.js';
	import hljs from 'highlight.js/lib/core';
	import 'highlight.js/styles/tomorrow-night-blue.css';
	import javascript from 'highlight.js/lib/languages/javascript';
	hljs.registerLanguage('javascript', javascript);

	const code = `// Fill all the elements with a value
const fruits = [ “Banana”, “Orange”, “Apple”, “Mango” ];
fruits.fill(“Kiwi”);

// Fill the last two elements
const fruits = [ “Banana”, “Orange”, “Apple”, “Mango” ];
fruits.fill(“Kiwi”, 2, 4);`;
	let createArray = $state('');
	createArray = hljs.highlight(code, { language: 'javascript' }).value;
</script>

<div class="mt-[-4.75rem] -mb-32 overflow-hidden bg-slate-900 pt-[4.75rem] pb-32">
	<div class="py-16 sm:px-2 lg:relative lg:px-0 lg:py-20">
		<div
			class="lg:max-w-8xl mx-auto grid max-w-2xl grid-cols-1 items-center gap-x-8 gap-y-16 px-4 lg:grid-cols-2 lg:px-8 xl:gap-x-16 xl:px-12"
		>
			<div class="relative z-10 md:text-center lg:text-left">
				<img
					alt=""
					role="presentation"
					loading="eager"
					width="1186"
					height="1186"
					class="absolute right-full bottom-full -mr-72 -mb-56 opacity-50"
					style="color:transparent"
					src="/blur-cyan.png"
				/>
				<div class="relative">
					<p
						class="font-display inline bg-linear-to-r from-indigo-200 via-sky-400 to-indigo-200 bg-clip-text text-5xl tracking-tight text-transparent"
					>
						JS visualized learning.
					</p>
					<p class="mt-3 text-2xl tracking-tight text-slate-400">
						Master JavaScript array methods through interactive visuals and hands-on examples.
					</p>
					<div class="mt-8 flex gap-4 md:justify-center lg:justify-start">
						<a
							class="rounded-full bg-sky-300 px-4 py-2 text-sm font-semibold text-slate-900 hover:bg-sky-200 focus:outline-hidden focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-sky-300/50 active:bg-sky-500"
							href="#{global_search[0]?.id}">Get started</a
						>
						<a
							class="rounded-full bg-slate-800 px-4 py-2 text-sm font-medium text-white hover:bg-slate-700 focus:outline-hidden focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-white/50 active:text-slate-400"
							href="https://github.com/jakebogan01/interactivejs">View on GitHub</a
						>
					</div>
				</div>
			</div>
			<div class="relative lg:static xl:pl-10">
				<div
					class="absolute inset-x-[-50vw] -top-32 -bottom-48 [mask-image:linear-gradient(transparent,white,transparent)] lg:-top-32 lg:right-0 lg:-bottom-32 lg:left-[calc(50%+14rem)] lg:[mask-image:linear-gradient(white,white,transparent)]"
				>
					<svg
						aria-hidden="true"
						viewBox="0 0 668 1069"
						width="668"
						height="1069"
						fill="none"
						class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 lg:left-0 lg:translate-x-0 lg:translate-y-[-60%]"
						><defs
							><clipPath id=":Rqja:-clip-path"
								><path fill="#fff" transform="rotate(-180 334 534.4)" d="M0 0h668v1068.8H0z"
								></path></clipPath
							></defs
						><g opacity=".4" clip-path="url(#:Rqja:-clip-path)" stroke-width="4"
							><path
								opacity=".3"
								d="M584.5 770.4v-474M484.5 770.4v-474M384.5 770.4v-474M283.5 769.4v-474M183.5 768.4v-474M83.5 767.4v-474"
								stroke="#334155"
							></path><path
								d="M83.5 221.275v6.587a50.1 50.1 0 0 0 22.309 41.686l55.581 37.054a50.102 50.102 0 0 1 22.309 41.686v6.587M83.5 716.012v6.588a50.099 50.099 0 0 0 22.309 41.685l55.581 37.054a50.102 50.102 0 0 1 22.309 41.686v6.587M183.7 584.5v6.587a50.1 50.1 0 0 0 22.31 41.686l55.581 37.054a50.097 50.097 0 0 1 22.309 41.685v6.588M384.101 277.637v6.588a50.1 50.1 0 0 0 22.309 41.685l55.581 37.054a50.1 50.1 0 0 1 22.31 41.686v6.587M384.1 770.288v6.587a50.1 50.1 0 0 1-22.309 41.686l-55.581 37.054A50.099 50.099 0 0 0 283.9 897.3v6.588"
								stroke="#334155"
							></path><path
								d="M384.1 770.288v6.587a50.1 50.1 0 0 1-22.309 41.686l-55.581 37.054A50.099 50.099 0 0 0 283.9 897.3v6.588M484.3 594.937v6.587a50.1 50.1 0 0 1-22.31 41.686l-55.581 37.054A50.1 50.1 0 0 0 384.1 721.95v6.587M484.3 872.575v6.587a50.1 50.1 0 0 1-22.31 41.686l-55.581 37.054a50.098 50.098 0 0 0-22.309 41.686v6.582M584.501 663.824v39.988a50.099 50.099 0 0 1-22.31 41.685l-55.581 37.054a50.102 50.102 0 0 0-22.309 41.686v6.587M283.899 945.637v6.588a50.1 50.1 0 0 1-22.309 41.685l-55.581 37.05a50.12 50.12 0 0 0-22.31 41.69v6.59M384.1 277.637c0 19.946 12.763 37.655 31.686 43.962l137.028 45.676c18.923 6.308 31.686 24.016 31.686 43.962M183.7 463.425v30.69c0 21.564 13.799 40.709 34.257 47.529l134.457 44.819c18.922 6.307 31.686 24.016 31.686 43.962M83.5 102.288c0 19.515 13.554 36.412 32.604 40.645l235.391 52.309c19.05 4.234 32.605 21.13 32.605 40.646M83.5 463.425v-58.45M183.699 542.75V396.625M283.9 1068.8V945.637M83.5 363.225v-141.95M83.5 179.524v-77.237M83.5 60.537V0M384.1 630.425V277.637M484.301 830.824V594.937M584.5 1068.8V663.825M484.301 555.275V452.988M584.5 622.075V452.988M384.1 728.537v-56.362M384.1 1068.8v-20.88M384.1 1006.17V770.287M283.9 903.888V759.85M183.699 1066.71V891.362M83.5 1068.8V716.012M83.5 674.263V505.175"
								stroke="#334155"
							></path><circle
								cx="83.5"
								cy="384.1"
								r="10.438"
								transform="rotate(-180 83.5 384.1)"
								fill="#1E293B"
								stroke="#334155"
							></circle><circle
								cx="83.5"
								cy="200.399"
								r="10.438"
								transform="rotate(-180 83.5 200.399)"
								stroke="#334155"
							></circle><circle
								cx="83.5"
								cy="81.412"
								r="10.438"
								transform="rotate(-180 83.5 81.412)"
								stroke="#334155"
							></circle><circle
								cx="183.699"
								cy="375.75"
								r="10.438"
								transform="rotate(-180 183.699 375.75)"
								fill="#1E293B"
								stroke="#334155"
							></circle><circle
								cx="183.699"
								cy="563.625"
								r="10.438"
								transform="rotate(-180 183.699 563.625)"
								fill="#1E293B"
								stroke="#334155"
							></circle><circle
								cx="384.1"
								cy="651.3"
								r="10.438"
								transform="rotate(-180 384.1 651.3)"
								fill="#1E293B"
								stroke="#334155"
							></circle><circle
								cx="484.301"
								cy="574.062"
								r="10.438"
								transform="rotate(-180 484.301 574.062)"
								fill="#0EA5E9"
								fill-opacity=".42"
								stroke="#0EA5E9"
							></circle><circle
								cx="384.1"
								cy="749.412"
								r="10.438"
								transform="rotate(-180 384.1 749.412)"
								fill="#1E293B"
								stroke="#334155"
							></circle><circle
								cx="384.1"
								cy="1027.05"
								r="10.438"
								transform="rotate(-180 384.1 1027.05)"
								stroke="#334155"
							></circle><circle
								cx="283.9"
								cy="924.763"
								r="10.438"
								transform="rotate(-180 283.9 924.763)"
								stroke="#334155"
							></circle><circle
								cx="183.699"
								cy="870.487"
								r="10.438"
								transform="rotate(-180 183.699 870.487)"
								stroke="#334155"
							></circle><circle
								cx="283.9"
								cy="738.975"
								r="10.438"
								transform="rotate(-180 283.9 738.975)"
								fill="#1E293B"
								stroke="#334155"
							></circle><circle
								cx="83.5"
								cy="695.138"
								r="10.438"
								transform="rotate(-180 83.5 695.138)"
								fill="#1E293B"
								stroke="#334155"
							></circle><circle
								cx="83.5"
								cy="484.3"
								r="10.438"
								transform="rotate(-180 83.5 484.3)"
								fill="#0EA5E9"
								fill-opacity=".42"
								stroke="#0EA5E9"
							></circle><circle
								cx="484.301"
								cy="432.112"
								r="10.438"
								transform="rotate(-180 484.301 432.112)"
								fill="#1E293B"
								stroke="#334155"
							></circle><circle
								cx="584.5"
								cy="432.112"
								r="10.438"
								transform="rotate(-180 584.5 432.112)"
								fill="#1E293B"
								stroke="#334155"
							></circle><circle
								cx="584.5"
								cy="642.95"
								r="10.438"
								transform="rotate(-180 584.5 642.95)"
								fill="#1E293B"
								stroke="#334155"
							></circle><circle
								cx="484.301"
								cy="851.699"
								r="10.438"
								transform="rotate(-180 484.301 851.699)"
								stroke="#334155"
							></circle><circle
								cx="384.1"
								cy="256.763"
								r="10.438"
								transform="rotate(-180 384.1 256.763)"
								stroke="#334155"
							></circle></g
						></svg
					>
				</div>
				<div class="relative">
					<img
						alt=""
						role="presentation"
						loading="eager"
						width="1186"
						height="1186"
						class="absolute -top-64 -right-64"
						style="color:transparent"
						src="/blur-cyan.png"
					/>
					<img
						alt=""
						role="presentation"
						loading="eager"
						width="1132"
						height="1134"
						class="absolute -right-44 -bottom-40"
						style="color:transparent"
						src="/blur-indigo.png"
					/>
					<div
						class="absolute inset-0 rounded-2xl bg-linear-to-tr from-sky-300 via-sky-300/70 to-blue-300 opacity-10 blur-lg"
					></div>
					<div
						class="absolute inset-0 rounded-2xl bg-linear-to-tr from-sky-300 via-sky-300/70 to-blue-300 opacity-10"
					></div>
					<div class="relative rounded-2xl bg-[#0A101F]/80 ring-1 ring-white/10 backdrop-blur-sm">
						<div
							class="absolute -top-px right-11 left-20 h-px bg-linear-to-r from-sky-300/0 via-sky-300/70 to-sky-300/0"
						></div>
						<div
							class="absolute right-20 -bottom-px left-11 h-px bg-linear-to-r from-blue-400/0 via-blue-400 to-blue-400/0"
						></div>
						<div class="pt-4 pl-4">
							<svg
								aria-hidden="true"
								viewBox="0 0 42 10"
								fill="none"
								class="h-2.5 w-auto stroke-slate-500/30"
								><circle cx="5" cy="5" r="4.5"></circle><circle cx="21" cy="5" r="4.5"
								></circle><circle cx="37" cy="5" r="4.5"></circle></svg
							>
							<div class="mt-6 flex items-start px-1 text-sm">
								<div
									aria-hidden="true"
									class="border-r border-slate-300/5 pr-4 font-mono text-slate-600 select-none"
								>
									01<br />02<br />03<br />04<br />05<br />06<br />07<br />
								</div>
								<pre class="!m-0 flex overflow-x-auto pb-6"><code
										class="hljs language-javascript !bg-transparent !p-0">{@html createArray}</code
									></pre>
							</div>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</div>
