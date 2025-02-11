<script>
	import { page } from '$app/state';

	let { page_title = null, description, keywords } = $props();
</script>

<svelte:head>
	<title>{`InteractiveJS${!page_title || ` - ${page_title}`}`}</title>
	<meta name="description" content={description} />
	<meta name="keywords" content={keywords} />
	<meta property="og:title" content="InteractiveJS" />
	<meta property="og:site_name" content={`InteractiveJS.dev`} />
	<meta property="og:url" content={page.url} />
	<meta property="og:description" content={description} />
	<meta property="og:type" content="website" />
	<meta property="og:image" content={'/og-image-interactivejs-1200x630.jpg'} />
</svelte:head>
