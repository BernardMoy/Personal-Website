<script lang="ts">
	// @ts-nocheck

	import projects from '../data/projects.json';
	import projectsTagsColors from '../data/projects-tags-colors.json';
	import projectsParagraph from '../data/projects-paragraph.json';
	import Rectangle from './Rectangle.svelte';
	import FadeIn from './FadeIn.svelte';

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

<div class="mx-12 flex flex-col gap-16 py-16 md:mx-16">
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
	<div class=" grid grid-cols-1 gap-8 md:grid-cols-3">
		<!-- individual project grid -->
		{#each displayedProjects as project, index}
			<FadeIn delay={200 * (index % ITEMS_PER_PAGE)}>
				<div class="relative flex w-full flex-col">
					<!-- Wrap hover transitions in an inner div, to prevent them being overridden by the fade in effect above -->
					<div
						class="h-full rounded-xl bg-on-primary pb-6 shadow-xl/50 shadow-holo-pink-shadow transition-transform ease-out hover:-translate-y-1 hover:duration-200"
					>
						<!-- image -->
						<div class="group relative">
							<img
								src={project.image}
								alt={project.title}
								class="h-[220px] w-full rounded-tl-xl rounded-tr-xl object-cover"
							/>

							<!-- overlay -->
							<div
								class="font-body absolute top-0 z-30 flex h-[220px] w-full origin-bottom scale-y-0 items-center justify-center rounded-tl-xl rounded-tr-xl bg-on-background/90 p-6 text-center text-[1rem]
						break-normal text-on-primary transition-transform duration-200 ease-out {overlayStates[index]
									? 'scale-y-100'
									: 'scale-y-0'}"
							>
								{project.description}
							</div>
						</div>

						<!-- title -->
						<div class="flex flex-row items-start justify-start gap-4 px-6 py-4">
							{#if project.github}
								<a
									class="group flex flex-row items-start justify-start gap-4 self-start"
									href={project.github}
									target="_blank"
								>
									<h1 class=" font-title relative text-[1.5rem] text-on-background">
										<!-- span wrapper to make the text inline -->
										<!-- so the sliding underline animation works when -->
										<!-- the text is broken into multiple lines -->
										<span class="project-title">
											{project.title}
										</span>
									</h1>

									<!-- github icon -->
									<svg width="28" height="27" fill="none" viewBox="0 0 28 27" class="mt-1 shrink-0"
										><path
											fill="var(--color-on-background)"
											class="transition-[fill] duration-[250ms] ease-out group-hover:fill-holo-pink group-focus:fill-holo-pink"
											d="M11.84 19.735c-3.61-.435-6.153-3.021-6.153-6.37 0-1.36.493-2.83 1.313-3.81-.355-.899-.3-2.804.11-3.594 1.093-.136 2.57.436 3.445 1.225 1.039-.326 2.133-.49 3.472-.49 1.34 0 2.434.164 3.418.463.848-.762 2.352-1.334 3.446-1.198.382.735.437 2.64.082 3.566.875 1.035 1.34 2.423 1.34 3.839 0 3.348-2.543 5.88-6.207 6.342.93.599 1.558 1.906 1.558 3.403v2.83c0 .817.684 1.28 1.504.953A13.8 13.8 0 0 0 28 13.992C28 6.288 21.71 0 13.973 0 6.234 0 0 6.288 0 13.992c0 6.043 3.855 11.051 9.05 12.93.74.272 1.45-.218 1.45-.953V23.79a3.5 3.5 0 0 1-1.313.272c-1.804 0-2.87-.98-3.636-2.803-.301-.735-.63-1.17-1.258-1.253-.328-.027-.438-.163-.438-.326 0-.327.547-.572 1.094-.572.793 0 1.477.49 2.188 1.497.547.79 1.12 1.144 1.804 1.144s1.121-.245 1.75-.872c.465-.462.82-.87 1.149-1.143"
										/></svg
									>
								</a>
							{:else}
								<div class="flex flex-row items-center justify-start gap-4">
									<h1 class="font-title glow relative text-[1.5rem] text-on-background">
										{project.title}
									</h1>
								</div>
							{/if}

							<!-- info icon -->
							<button
								class="ml-auto shrink-0 cursor-pointer"
								aria-label="Info"
								onclick={() => handleInfoClick(index)}
							>
								<svg
									width="28"
									height="28"
									fill="none"
									viewBox="0 0 28 28"
									class="my-1 h-[28px] w-[28px] rounded-full {overlayStates[index]
										? 'outline-4 outline-yellow-highlight'
										: 'hover:outline-4 hover:outline-gray-highlight focus:outline-4 focus:outline-gray-highlight active:outline-yellow-highlight'}"
									><path
										fill="var(--color-holo-pink)"
										d="M23.906 4.107c-5.464-5.471-14.329-5.477-19.8-.013-5.47 5.464-5.476 14.329-.012 19.8 5.464 5.47 14.329 5.476 19.8.012 5.47-5.464 5.476-14.329.012-19.8m-7.951 18.777a.39.39 0 0 1-.391.39h-3.128a.39.39 0 0 1-.39-.39v-11.61a.39.39 0 0 1 .39-.391h3.128a.39.39 0 0 1 .39.39zM14 9.26a2.27 2.27 0 0 1-2.267-2.267A2.27 2.27 0 0 1 14 4.725a2.27 2.27 0 0 1 2.267 2.268A2.27 2.27 0 0 1 14 9.26"
									/></svg
								>
							</button>
						</div>

						<!-- tags -->
						<ul class="flex max-w-full flex-wrap gap-x-4 gap-y-2 px-6">
							{#each project.tags as tag}
								<li
									class="font-body px-2 text-[1rem] text-on-background"
									style="background-color: {projectsTagsColors[tag]
										? projectsTagsColors[tag]
										: projectsTagsColors['default']}"
								>
									{tag}
								</li>
							{/each}
						</ul>
					</div>
				</div>
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

<style>
	.project-title {
		box-decoration-break: clone;
		background: linear-gradient(to right, var(--color-holo-pink), var(--color-holo-pink));

		background-size: 0% 0.1em;
		background-position: 0% 100%;
		background-repeat: no-repeat;

		transition:
			background-size 250ms ease-out,
			color 250ms ease-out;
	}

	.group:hover .project-title,
	.group:focus .project-title {
		background-size: 100% 0.1em;
		color: var(--color-holo-pink);
	}
</style>
