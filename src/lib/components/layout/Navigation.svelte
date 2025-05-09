<script lang="ts">
	import { page } from '$app/state';
	import type { navProps } from '$lib/navigation';
	import Logo from '../Logo.svelte';
	import ThemeToggle from '../ThemeToggle.svelte';

	let isActive = $state(false);
	const toggleNav = () => (isActive = !isActive);

	let currentPagePath = $derived(page.url.pathname);
	let { navType, routes }: navProps = $props();
</script>

<header id="main-header" class="main-header">
	<div class="main-header__container">
		<a id="logo" class="main-header__logo" href="/">
			<Logo />
		</a>

		<nav class="main-header__nav" class:active={isActive}>
			<ul class="main-header__nav-links">
				<!-- top level routes -->
				{#each routes as route}
					<li
						class="main-header__nav-item"
						class:main-header__nav-item--active={currentPagePath.startsWith(route.path)}
					>
						<a
							class="main-header__nav-link"
							class:main-header__nav-link--active={currentPagePath.startsWith(route.path)}
							id="main-header__nav-link-{route.name.toLowerCase()}"
							href={route.path}
						>
							{route.name}
						</a>

						<!-- 2nd level routes -->
						{#if route.children?.length}
							<ul class="main-header__nav-sub-links">
								{#each route.children as subroute}
									<li class="main-header__nav-sub-item">
										<a href="/" class="main-header__nav-sub-link">
											{subroute.name}
										</a>
									</li>
								{/each}
							</ul>
						{/if}
					</li>
				{/each}
			</ul>
		</nav>

		<div class="main-header__mod">
			<ThemeToggle />
			<button
				id="nav-toggle"
				aria-label="Toggle"
				class:active={isActive}
				aria-expanded={isActive}
				onclick={toggleNav}
			>
				<span />
				<span />
				<span />
			</button>

			<a href="/" class="btn">Contact</a>
		</div>
	</div>
</header>
