<script lang="ts">
	import './styles.less';
	import type { LayoutProps } from './$types';
	import Navigation from '$lib/components/layout/Navigation.svelte';
	import Footer from '$lib/components/layout/Footer.svelte';
	import { getNavRoutes } from '$lib/navigation';

	const { children }: LayoutProps = $props();
	const routes = getNavRoutes('public');
</script>

<!-- theme -->
<svelte:head>
	<script>
		{
			const theme = localStorage.getItem('sv:theme');

			document.documentElement.classList.add(
				!theme || theme === 'system'
					? window.matchMedia('(prefers-color-scheme: dark)').matches
						? 'dark'
						: 'light'
					: theme
			);
		}
	</script>
</svelte:head>

<Navigation navType="public" {routes} />

<main>
	{@render children()}
</main>
<Footer />
