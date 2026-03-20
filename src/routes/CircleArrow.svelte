<script lang="ts">
	import { onMount } from 'svelte';
	import navigations from '../data/navigations.json';
	let { scrollindex, onclick }: { scrollindex: number; onclick: () => void } = $props();

	var arrow: HTMLElement | null;
	onMount(() => {
		arrow = document.getElementById('circle-arrow');
	});

	// when the scrollIndex reaches the last index (i.e. the user scrolled to the last section)
	// then rotate the svg to point back up
	$effect(() => {
		if (scrollindex === navigations.length - 1) {
			arrow?.classList.add('rotate-180');
		} else {
			arrow?.classList.remove('rotate-180');
		}
	});
</script>

<button
	class="group flex h-[48px] w-[48px] items-center justify-center rounded-full
	border-1 border-on-primary bg-primary shadow-xl/50 shadow-primary
	transition-transform duration-300 ease-out hover:-translate-y-1 hover:cursor-pointer"
	aria-label="next page"
	{onclick}
>
	<!-- wrap in a div to enable scaling of the arrow down icon -->
	<div class="h-[15px] w-[28px] duration-300 ease-out group-active:scale-80" id="circle-arrow">
		<svg fill="none" viewBox="0 0 28 15"
			><path
				fill="#fff"
				fill-rule="evenodd"
				d="M28 1.896 26.032 0l-12.05 11.265-1.285-1.202.007.007L1.998.061 0 1.928C2.958 4.695 11.22 12.418 13.982 15c2.052-1.917.052-.047 14.018-13.104"
				clip-rule="evenodd"
			/></svg
		>
	</div>
</button>
