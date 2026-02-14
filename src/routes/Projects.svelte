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
				<img
					src={project.image}
					alt={project.title}
					class="h-[220px] w-full rounded-tl-xl rounded-tr-xl object-cover"
				/>

				<!-- title -->
				{#if project.github}
					<a
						class="flex flex-row items-center justify-start gap-4 self-start px-6 py-4 decoration-on-background decoration-[1px] underline-offset-4 hover:underline"
						href={project.github}
						target="_blank"
					>
						<h1 class="font-title relative text-[24px] text-on-background">
							{project.title}
						</h1>
						<img src="svgs/github.svg" alt="GitHub link" , class="h-[24px] w-[24px]" />
					</a>
				{:else}
					<div class="flex flex-row items-center justify-start gap-4 px-6 py-4">
						<h1 class="font-title relative text-[24px] text-on-background">
							{project.title}
						</h1>
					</div>
				{/if}

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
