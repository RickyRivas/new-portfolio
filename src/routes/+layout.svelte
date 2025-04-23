<script lang="ts">
	import './styles.less';
	import type { LayoutProps } from './$types';
	import Navigation from '$lib/components/layout/Navigation.svelte';
	import Footer from '$lib/components/layout/Footer.svelte';
	const { children }: LayoutProps = $props();
</script>

<Navigation />
<main>
	{@render children()}
</main>
<Footer />
