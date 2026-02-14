<script>
	// @ts-nocheck

	import projects from '../data/projects.json';
	import projectsTagsColors from '../data/projects-tags-colors.json';
</script>

<div class="mx-16 flex flex-col gap-16 py-16">
	<!-- intro paragraph -->
	<p class="font-body text-[18px] text-on-background">
		Here is a list of technical projects that I have done.
	</p>

	<!-- project list -->
	<div class=" grid grid-cols-3 gap-8">
		<!-- individual project grid -->
		{#each projects as project}
			<div class="relative flex w-full flex-col rounded-xl bg-on-primary pb-6">
				<!-- image -->
				<div class="group relative">
					<img
						src={project.image}
						alt={project.title}
						class="h-[220px] w-full rounded-tl-xl rounded-tr-xl object-cover"
					/>

					<!-- overlay -->
					<div
						class="font-body absolute top-0 z-30 flex h-[220px] w-full origin-bottom scale-y-0 items-center justify-center rounded-tl-xl rounded-tr-xl bg-on-background/90 p-6 text-center text-[18px]
						break-normal text-on-primary transition-transform duration-200 ease-out"
					>
						{project.description}
					</div>
				</div>

				<!-- title -->
				<div class="flex flex-row items-start justify-start gap-4 px-6 py-4">
					{#if project.github}
						<a
							class="flex flex-row items-start justify-start gap-4 self-start decoration-on-background decoration-[1px] underline-offset-4 hover:underline"
							href={project.github}
							target="_blank"
						>
							<h1 class="font-title relative text-[24px] text-on-background">
								{project.title}
							</h1>

							<!-- github icon -->
							<img src="svgs/github.svg" alt="GitHub link" , class="mt-1 h-[24px] w-[24px]" />
						</a>
					{:else}
						<div class="flex flex-row items-center justify-start gap-4">
							<h1 class="font-title relative text-[24px] text-on-background">
								{project.title}
							</h1>
						</div>
					{/if}

					<!-- info icon -->
					<img src="svgs/info.svg" alt="GitHub link" , class="mt-1 ml-auto h-[24px] w-[24px]" />
				</div>

				<!-- tags -->
				<ul class="flex max-w-full flex-wrap gap-x-4 gap-y-2 px-6">
					{#each project.tags as tag}
						<li
							class="font-body px-2 text-[18px] text-on-background"
							style="background-color: {projectsTagsColors[tag]
								? projectsTagsColors[tag]
								: projectsTagsColors['default']}"
						>
							{tag}
						</li>
					{/each}
				</ul>
			</div>
		{/each}
	</div>
</div>

<style>
	.overlay {
		transform: scaleY(0);
		transform-origin: bottom;
		transition: transform 0.4s ease;
	}

	.overlay:hover {
		transform: scaleY(1);
	}
</style>
