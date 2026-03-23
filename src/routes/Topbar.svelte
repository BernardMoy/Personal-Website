<script lang="ts">
	import navigations from '../data/navigations.json';

	function handleHeaderClick(navigationId: string) {
		const element = document.getElementById(navigationId);
		element?.scrollIntoView({
			behavior: 'smooth'
		});
	}
</script>

<!-- currently it has a fixed height of 80px with z=50 -->
<header
	class="no-selection fixed top-0 z-50 flex h-[80px] w-full flex-row items-center justify-between bg-main/75 px-8 md:justify-start md:gap-16 md:px-16"
>
	{#each navigations as { name, navigationId, color }}
		<button
			class="font-title text-[1rem] hover:cursor-pointer"
			onclick={() => handleHeaderClick(navigationId)}
			><span class="sections" style={`--hover-color: ${color};`}>{name}</span>
		</button>
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

	/* when the top bar items are hovered, change the color and grow the background from center horizontally */
	.sections:hover {
		background-size: 100% 0.1em;
		color: var(--hover-color);
	}

	/* when the items are clicked active on mobile, perform the same for now */
	.sections:active {
		background-size: 100% 0.1em;
		color: var(--hover-color);
	}
</style>
