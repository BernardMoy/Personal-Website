<script>
	import navigations from '../data/navigations.json';
</script>

<!-- currently it has a fixed height of 80px with z=50 -->
<header
	class="no-selection fixed top-0 z-50 flex h-[80px] w-full flex-row items-center gap-16 bg-white/75 px-16"
>
	{#each navigations as { name, navigationId, color }}
		<a href={navigationId} class="font-title text-[16px]"
			><span class="sections" style={`--hover-color: ${color};`}>{name}</span></a
		>
	{/each}
</header>

<style>
	.sections {
		box-decoration-break: clone;
		background: linear-gradient(to right, var(--hover-color), var(--hover-color));

		background-size: 0% 0.1em;
		background-position: 50% 100%; /* grow from the center horizontally */
		background-repeat: no-repeat;

		transition:
			background-size 250ms ease-out,
			color 250ms ease-out;
	}

	.sections:hover {
		background-size: 100% 0.1em;
		color: var(--hover-color);
	}
</style>
