<script>
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

				<!-- github logo -->
				{#if project.github}
					<a href={project.github} target="_blank" class="cursor-pointer" aria-label="github link">
						<img
							src="svgs/github-white.svg"
							alt="github logo"
							class="absolute top-2 right-2 h-[64px] w-[64px]"
						/>
					</a>
				{/if}

				<!-- title -->
				<h1 class="font-title relative px-6 py-4 text-[24px] text-on-background">
					{project.title}
				</h1>

				<!-- tags -->
				<ul class="flex max-w-full flex-wrap gap-x-4 gap-y-2 px-6">
					{#each project.tags as tag}
						<li
							class="font-body px-2 text-[18px] text-on-background"
							style="background-color: {projectsTagsColors[tag]}"
						>
							{tag}
						</li>
					{/each}
				</ul>
			</div>
		{/each}
	</div>
</div>
