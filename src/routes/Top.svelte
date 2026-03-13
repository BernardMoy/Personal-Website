<script lang="ts">
	import Circle from './Circle.svelte';
	import top from '../data/top.json';
	import backgrounds from '../data/backgrounds.json';
	import { fade, scale } from 'svelte/transition';
	import { onMount } from 'svelte';

	// the scrollIndex is passed from the root page to here
	// to stop the transition when it is not 0 (Top)
	let props = $props();

	// the current index of the image displayed
	var currentIndex = $state<number>(0);

	// store the interval to display images one by one automatically
	var interval: NodeJS.Timeout;
	var progressBar: HTMLElement | null;

	function createInterval() {
		interval = setInterval(() => {
			// display the next image
			setIndex((currentIndex + 1) % backgrounds.length);
		}, 8000);
	}

	function setIndex(index: number) {
		currentIndex = index;

		// change the primary color to match the index
		document.documentElement.style.setProperty(
			'--color-primary',
			backgrounds[index]['primary-color']
		);

		// reset the progress bar
		// instantly go from scale 100 to scale 0
		progressBar?.classList.remove('transition-transform');
		progressBar?.classList.add('transition-none');
		progressBar?.classList.remove('scale-x-100');
		progressBar?.classList.add('scale-x-0');
		progressBar?.offsetHeight; // refresh the element
		// scale 0 to 100 in _ seconds
		progressBar?.classList.remove('transition-none');
		progressBar?.classList.add('transition-transform');
		progressBar?.classList.remove('scale-x-0');
		progressBar?.classList.add('scale-x-100');

		// reset the interval
		if (interval) {
			clearInterval(interval);
			createInterval();
		}
	}

	// increments the index every certain seconds
	onMount(() => {
		progressBar = document.getElementById('progress-bar');
		// createInterval();

		// set index to instantly trigger the effects
		setIndex(0);

		return () => clearInterval(interval);
	});

	// clear the interval when the scroll index is not 0
	$effect(() => {
		const index = props.scrollIndex;
		// re-create the interval if index changes to 0, else clear it
		if (interval) {
			clearInterval(interval);
		}
		if (index === 0) {
			createInterval(); // also handles the initial creation, when the page lands at scroll index = 0
		}
	});
</script>

<div class="relative h-screen w-full overflow-x-clip text-center">
	<!-- large background image -->
	{#key currentIndex}
		<img
			src={backgrounds[currentIndex].url}
			alt={backgrounds[currentIndex].name}
			class="absolute top-0 left-0 h-screen w-full object-cover"
			in:scale={{ start: 1.05, duration: 1500 }}
			out:fade={{ duration: 1000 }}
		/>
	{/key}

	<!-- centered text -->
	<div class="absolute top-1/2 z-24 flex w-full -translate-y-1/2 flex-col items-center">
		<h1 class="glow-primary font-main-title text-[64px] text-on-primary">{top.title}</h1>
		<h2 class="glow-primary font-main-title text-[36px] text-on-primary">{top.subtitle}</h2>
	</div>

	<!-- number buttons on the left -->
	<div class="no-selection absolute top-0 z-26 m-4 mt-[96px] flex flex-col gap-4">
		{#each { length: backgrounds.length } as _, i}
			<Circle
				text={(i + 1).toString()}
				onclick={() => {
					setIndex(i);
				}}
				selected={i == currentIndex}
			></Circle>
		{/each}
	</div>

	<!-- the rectangles on the top right displayed in 2 columns -->
	<div class="absolute top-0 right-0 z-25 mt-[80px] flex flex-col">
		<div class="no-selection grid grid-cols-2">
			{#each backgrounds as bg, index}
				<!-- scale within container -->
				<button
					aria-label={bg.name}
					class="group h-[64px] w-[160px] cursor-pointer overflow-hidden"
					onclick={() => setIndex(index)}
				>
					<img
						src={bg.url}
						alt={bg.name}
						class="h-full w-full object-cover object-center duration-500 group-hover:scale-110"
					/>
				</button>
			{/each}
		</div>

		<!-- Progress bar -->
		<div
			id="progress-bar"
			class=" no-selection h-1 w-full origin-left scale-x-0 bg-on-primary opacity-75
			shadow-2xl/50 shadow-primary transition-transform
			duration-7500 ease-linear"
		></div>
	</div>
</div>

<style>
	/* the glow for title */
	.glow-primary {
		text-shadow:
			0px 0px 32px var(--color-primary),
			0px 0px 16px var(--color-primary),
			0px 0px 8px var(--color-primary);
	}
</style>
