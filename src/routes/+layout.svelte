<script lang="ts">
	import './styles.less';
	import type { LayoutProps } from './$types';
	const { children }: LayoutProps = $props();
</script>

{@render children()}
