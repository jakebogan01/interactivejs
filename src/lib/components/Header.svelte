<script>
	import { onMount } from 'svelte';
	import { HOME } from '$lib/utils/links.js';
	import { global_data } from '$lib/stores/globalData.svelte.js';

	let { scrollY } = $state(0);

	const opacity = $derived.by(() => {
		return Math.min(scrollY / 100, 0.75);
	});

	let isScrolling;
	const handleScroll = () => {
		if (isScrolling) {
			window.cancelAnimationFrame(isScrolling);
		}
		isScrolling = window.requestAnimationFrame(() => {
			scrollY = window.scrollY;
		});
	};

	onMount(() => {
		handleScroll();
		window.addEventListener('scroll', handleScroll);
		return () => {
			window.removeEventListener('scroll', handleScroll);
		};
	});
</script>

<header
	class="sticky top-0 z-50 flex flex-none flex-wrap items-center justify-between bg-slate-900/95 px-4 py-5 transition duration-500 sm:px-6 lg:px-8 {opacity >
	0
		? 'backdrop-blur-sm'
		: 'backdrop-blur-0'}"
	style={`background-color: rgba(14, 23, 44, ${opacity || 0});`}
>
	<!--		<div class="mr-6 flex lg:hidden">-->
	<!--			<button type="button" class="relative" aria-label="Open navigation">-->
	<!--				<svg aria-hidden="true" viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round" class="h-6 w-6 stroke-slate-500"><path d="M4 7h16M4 12h16M4 17h16"></path></svg>-->
	<!--			</button>-->
	<!--		</div>-->
	<div class="relative flex grow basis-0 items-center">
		<a aria-label="Home page" href={HOME}>
			<svg
				aria-hidden="true"
				xmlns="http://www.w3.org/2000/svg"
				width="135.034"
				height="24"
				viewBox="0 0 135.034 24"
				><g transform="translate(-258 -255)"
					><g transform="translate(168.833 187.292)"
						><path
							d="M1.533-2.992V-14.2H3.815v9.3H9.488v1.9ZM15.839-5.6,18-5.235a3.54,3.54,0,0,1-1.314,1.808,3.861,3.861,0,0,1-2.247.62,3.662,3.662,0,0,1-3.16-1.4,4.687,4.687,0,0,1-.809-2.821A4.52,4.52,0,0,1,11.53-10.21a3.5,3.5,0,0,1,2.69-1.152A3.634,3.634,0,0,1,17.1-10.156a5.337,5.337,0,0,1,1.01,3.7H12.687a2.191,2.191,0,0,0,.524,1.5,1.639,1.639,0,0,0,1.249.536,1.326,1.326,0,0,0,.856-.277A1.714,1.714,0,0,0,15.839-5.6Zm.123-2.189a2.085,2.085,0,0,0-.486-1.43,1.49,1.49,0,0,0-1.125-.489,1.5,1.5,0,0,0-1.172.516,2,2,0,0,0-.455,1.4ZM21.5-8.68l-1.966-.355a3.061,3.061,0,0,1,1.141-1.757,4.175,4.175,0,0,1,2.4-.57,5.183,5.183,0,0,1,2.158.343,2.153,2.153,0,0,1,1,.871,4.466,4.466,0,0,1,.289,1.939L26.5-5.682a8.777,8.777,0,0,0,.1,1.592,4.646,4.646,0,0,0,.389,1.1H24.85q-.085-.216-.208-.64-.054-.193-.077-.254a3.9,3.9,0,0,1-1.187.809,3.4,3.4,0,0,1-1.349.27,2.789,2.789,0,0,1-1.992-.686,2.28,2.28,0,0,1-.728-1.734,2.328,2.328,0,0,1,.331-1.237,2.166,2.166,0,0,1,.929-.832,7.259,7.259,0,0,1,1.723-.5,11.8,11.8,0,0,0,2.1-.532v-.216a1.121,1.121,0,0,0-.308-.89,1.848,1.848,0,0,0-1.164-.266,1.55,1.55,0,0,0-.9.227A1.58,1.58,0,0,0,21.5-8.68Zm2.9,1.757a13.538,13.538,0,0,1-1.318.331,3.97,3.97,0,0,0-1.179.378.9.9,0,0,0-.424.763,1.062,1.062,0,0,0,.339.786,1.184,1.184,0,0,0,.863.331,1.876,1.876,0,0,0,1.118-.385,1.357,1.357,0,0,0,.516-.717,4.277,4.277,0,0,0,.085-1.056Zm6.336,3.931H28.565v-8.186h2.012v1.164a3.5,3.5,0,0,1,.929-1.087,1.709,1.709,0,0,1,.937-.262,2.749,2.749,0,0,1,1.426.409L33.2-9.066A1.9,1.9,0,0,0,32.18-9.42a1.2,1.2,0,0,0-.771.251,1.712,1.712,0,0,0-.5.906,12.866,12.866,0,0,0-.181,2.744Zm11.516,0H40.08V-7.17a6.457,6.457,0,0,0-.139-1.715,1.2,1.2,0,0,0-.451-.605,1.289,1.289,0,0,0-.752-.216,1.737,1.737,0,0,0-1.01.308,1.553,1.553,0,0,0-.613.817A7.062,7.062,0,0,0,36.951-6.7v3.707H34.785v-8.186H36.8v1.2a3.278,3.278,0,0,1,2.7-1.387,3.25,3.25,0,0,1,1.31.258,2.2,2.2,0,0,1,.9.659,2.387,2.387,0,0,1,.424.91,6.765,6.765,0,0,1,.119,1.457Z"
							transform="translate(120 87.975)"
							fill="#fff"
						/><path
							d="M4.029-3.114-.01-14.316H2.464l2.86,8.291,2.767-8.291h2.42L6.465-3.114Zm7.346-9.215v-1.987h2.166v1.987Zm0,9.215v-8.115h2.166v8.115ZM15-5.43l2.174-.329a1.576,1.576,0,0,0,.563.951,1.913,1.913,0,0,0,1.187.325,2.157,2.157,0,0,0,1.264-.306.68.68,0,0,0,.285-.573.561.561,0,0,0-.154-.4,1.734,1.734,0,0,0-.725-.283A11.755,11.755,0,0,1,16.269-7.1,2.086,2.086,0,0,1,15.3-8.922a2.243,2.243,0,0,1,.84-1.773,3.948,3.948,0,0,1,2.605-.718,4.577,4.577,0,0,1,2.5.543,2.773,2.773,0,0,1,1.125,1.6l-2.043.374a1.252,1.252,0,0,0-.5-.726,1.83,1.83,0,0,0-1.044-.252,2.37,2.37,0,0,0-1.226.237.508.508,0,0,0-.247.436.473.473,0,0,0,.216.39,8.177,8.177,0,0,0,2.023.6,6.052,6.052,0,0,1,2.416.955,1.977,1.977,0,0,1,.678,1.6,2.443,2.443,0,0,1-.94,1.918,4.188,4.188,0,0,1-2.783.8A4.6,4.6,0,0,1,16.273-3.6,3.1,3.1,0,0,1,15-5.43Zm14.93,2.315V-4.329a3.147,3.147,0,0,1-1.175,1.024,3.318,3.318,0,0,1-1.538.374,3.028,3.028,0,0,1-1.48-.359A2.128,2.128,0,0,1,24.787-4.3a4.466,4.466,0,0,1-.293-1.8v-5.135H26.66V-7.5a10.253,10.253,0,0,0,.119,2.1,1.144,1.144,0,0,0,.435.611,1.347,1.347,0,0,0,.8.225,1.715,1.715,0,0,0,.994-.3,1.538,1.538,0,0,0,.6-.749,8.619,8.619,0,0,0,.162-2.189v-3.423h2.166v8.115ZM35.8-8.754l-1.966-.351a3.033,3.033,0,0,1,1.141-1.742,4.2,4.2,0,0,1,2.4-.565,5.223,5.223,0,0,1,2.158.34,2.147,2.147,0,0,1,1,.863,4.393,4.393,0,0,1,.289,1.922L40.8-5.781a8.627,8.627,0,0,0,.1,1.578A4.579,4.579,0,0,0,41.3-3.114H39.154q-.085-.214-.208-.634Q38.892-3.94,38.869-4a3.907,3.907,0,0,1-1.187.8,3.425,3.425,0,0,1-1.349.267,2.8,2.8,0,0,1-1.992-.68,2.251,2.251,0,0,1-.728-1.719,2.293,2.293,0,0,1,.331-1.226,2.159,2.159,0,0,1,.929-.825,7.307,7.307,0,0,1,1.723-.5,11.884,11.884,0,0,0,2.1-.527v-.214a1.106,1.106,0,0,0-.308-.883,1.86,1.86,0,0,0-1.164-.264,1.56,1.56,0,0,0-.9.225A1.566,1.566,0,0,0,35.8-8.754Zm2.9,1.742q-.416.138-1.318.329a3.994,3.994,0,0,0-1.179.374.894.894,0,0,0-.424.756,1.049,1.049,0,0,0,.339.779,1.19,1.19,0,0,0,.863.329A1.886,1.886,0,0,0,38.1-4.826a1.345,1.345,0,0,0,.516-.711A4.2,4.2,0,0,0,38.7-6.584Zm4.262,3.9v-11.2h2.166v11.2Zm4.386,0v-11.2h2.166v11.2Zm3.361-8.115h2.3l1.958,5.761,1.912-5.761h2.243L56.235-3.42l-.516,1.414a5.743,5.743,0,0,1-.543,1.085,2.36,2.36,0,0,1-.594.607,2.606,2.606,0,0,1-.825.363,4.318,4.318,0,0,1-1.106.13,5.787,5.787,0,0,1-1.226-.13l-.193-1.681a4.832,4.832,0,0,0,.917.1,1.365,1.365,0,0,0,1.118-.439,3.039,3.039,0,0,0,.555-1.119Z"
							transform="translate(165.076 88)"
							fill="#00a6f4"
						/></g
					><g transform="translate(87 51)"
						><circle cx="12" cy="12" r="12" transform="translate(171 204)" fill="#00a6f4" /><path
							d="M14.178,8.972H11.011a.122.122,0,0,1-.069-.027.1.1,0,0,1-.017-.068h0a3.241,3.241,0,0,0-.872-2.14,2.71,2.71,0,0,0-4.005,0,3.231,3.231,0,0,0-.869,2.143c0,.01,0,.019,0,.029a.072.072,0,0,1-.016.039.122.122,0,0,1-.07.027H1.954a.159.159,0,0,1-.078-.027.116.116,0,0,1-.033-.059A7.009,7.009,0,0,1,1.9,8.1L.152,6.612a.477.477,0,0,1-.094-.576l1.655-3.1a.414.414,0,0,1,.359-.222.387.387,0,0,1,.149.03l2.057.9a6.254,6.254,0,0,1,1.4-.884L5.98.384A.442.442,0,0,1,6.394,0H9.7a.44.44,0,0,1,.414.372l.308,2.371a5.991,5.991,0,0,1,1.4.885l2.055-.9a.388.388,0,0,1,.149-.03.415.415,0,0,1,.359.222l1.655,3.1a.477.477,0,0,1-.095.576L14.2,8.087a7.382,7.382,0,0,1,.058.821.087.087,0,0,1-.017.037.1.1,0,0,1-.06.027Z"
							transform="translate(175.077 207.791)"
							fill="#fff"
						/><path
							d="M17.135,36.5s.77-.052,1.027.379.16.714,0,1.345c-.9,3.547-4.525,6.24-8.862,6.24A8.959,8.959,0,0,1,.43,38.187c-.143-.535-.271-.888,0-1.31S1.515,36.5,1.515,36.5Z"
							transform="translate(173.83 181.529)"
							fill="#fff"
						/></g
					></g
				></svg
			>
		</a>
	</div>
	<div class="-my-5 mr-6 sm:mr-8 md:mr-0">
		<button
			onclick={() => (global_data.active = 'search')}
			type="button"
			class="group flex h-6 w-6 items-center justify-center sm:justify-start md:h-auto md:w-80 md:flex-none md:rounded-lg md:bg-slate-800/75 md:py-2.5 md:pr-3.5 md:pl-4 md:text-sm md:ring-1 md:ring-white/5 md:ring-inset md:hover:bg-slate-700/40 md:hover:ring-slate-500 lg:w-96"
		>
			<svg
				aria-hidden="true"
				viewBox="0 0 20 20"
				class="h-5 w-5 flex-none fill-slate-500 group-hover:fill-slate-500 md:group-hover:fill-slate-400"
				><path
					d="M16.293 17.707a1 1 0 0 0 1.414-1.414l-1.414 1.414ZM9 14a5 5 0 0 1-5-5H2a7 7 0 0 0 7 7v-2ZM4 9a5 5 0 0 1 5-5V2a7 7 0 0 0-7 7h2Zm5-5a5 5 0 0 1 5 5h2a7 7 0 0 0-7-7v2Zm8.707 12.293-3.757-3.757-1.414 1.414 3.757 3.757 1.414-1.414ZM14 9a4.98 4.98 0 0 1-1.464 3.536l1.414 1.414A6.98 6.98 0 0 0 16 9h-2Zm-1.464 3.536A4.98 4.98 0 0 1 9 14v2a6.98 6.98 0 0 0 4.95-2.05l-1.414-1.414Z"
				></path></svg
			>
			<span class="sr-only md:not-sr-only md:ml-2 md:text-slate-400">Search docs</span>
		</button>
	</div>
	<div class="relative flex basis-0 justify-end gap-6 sm:gap-8 md:grow">
		<a class="group" aria-label="GitHub" href="https://github.com/jakebogan01/interactivejs">
			<svg
				aria-hidden="true"
				viewBox="0 0 16 16"
				class="h-6 w-6 fill-slate-400 group-hover:fill-slate-300"
				><path
					d="M8 0C3.58 0 0 3.58 0 8C0 11.54 2.29 14.53 5.47 15.59C5.87 15.66 6.02 15.42 6.02 15.21C6.02 15.02 6.01 14.39 6.01 13.72C4 14.09 3.48 13.23 3.32 12.78C3.23 12.55 2.84 11.84 2.5 11.65C2.22 11.5 1.82 11.13 2.49 11.12C3.12 11.11 3.57 11.7 3.72 11.94C4.44 13.15 5.59 12.81 6.05 12.6C6.12 12.08 6.33 11.73 6.56 11.53C4.78 11.33 2.92 10.64 2.92 7.58C2.92 6.71 3.23 5.99 3.74 5.43C3.66 5.23 3.38 4.41 3.82 3.31C3.82 3.31 4.49 3.1 6.02 4.13C6.66 3.95 7.34 3.86 8.02 3.86C8.7 3.86 9.38 3.95 10.02 4.13C11.55 3.09 12.22 3.31 12.22 3.31C12.66 4.41 12.38 5.23 12.3 5.43C12.81 5.99 13.12 6.7 13.12 7.58C13.12 10.65 11.25 11.33 9.47 11.53C9.76 11.78 10.01 12.26 10.01 13.01C10.01 14.08 10 14.94 10 15.21C10 15.42 10.15 15.67 10.55 15.59C13.71 14.53 16 11.53 16 8C16 3.58 12.42 0 8 0Z"
				></path></svg
			>
		</a>
	</div>
</header>
