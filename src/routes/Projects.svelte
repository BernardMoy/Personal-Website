<!-- Content of the projects section -->
<script lang="ts">
	// @ts-nocheck

	import projects from '../data/projects.json';
	import projectsTagsColors from '../data/projects-tags-colors.json';
	import projectsParagraph from '../data/projects-paragraph.json';
	import Rectangle from './Rectangle.svelte';
	import FadeIn from './FadeIn.svelte';
	import { asset } from '$app/paths';
	import ProjectsItem from './ProjectsItem.svelte';

	// stores a list of indices with overlay turned on, initially all false
	let overlayStates = $state(new Array<boolean>(projects.length).fill(false));

	// function when info button is clicked, to toggle the overlay states
	const handleInfoClick = (index: number) => {
		overlayStates[index] = !overlayStates[index];
	};

	// number of projects to display vertically, cols 1, per page
	const ITEMS_PER_PAGE = 6;
	let limit = $state(ITEMS_PER_PAGE);
	let displayedProjects = $derived(projects.slice(0, limit));
</script>

<div class="z-2 mx-8 flex flex-col gap-8 py-8 sm:mx-16 sm:gap-16 sm:py-16">
	<!-- intro paragraph -->
	<FadeIn delay={500}>
		<div class="flex flex-col items-start justify-start gap-8">
			{#each projectsParagraph as para}
				<p class="font-body glow text-[1rem] text-on-background">
					{@html para.replaceAll('[', '<span class="text-holo-pink">').replaceAll(']', '</span>')}
				</p>
			{/each}
		</div>
	</FadeIn>

	<!-- project list -->
	<div class=" grid grid-cols-1 gap-8 md:grid-cols-2 lg:grid-cols-3">
		<!-- individual project grid -->
		{#each displayedProjects as project, index}
			<FadeIn delay={200 * (index % ITEMS_PER_PAGE)}>
				<ProjectsItem {project} {overlayStates} {index}></ProjectsItem>
			</FadeIn>
		{/each}
	</div>

	<!-- the show more button -->
	<div class="mx-auto shrink items-center">
		{#if limit !== projects.length}
			<Rectangle
				text="Show more"
				onclick={() => {
					// increase the limit by 6, or until max is reached
					limit = Math.min(limit + ITEMS_PER_PAGE, projects.length);

					console.log(limit);
					console.log(projects.length);
				}}
			/>
		{/if}
	</div>
</div>
