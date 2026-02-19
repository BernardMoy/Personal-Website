<script>
	import skills from '../data/skills.json';
	import aboutMe from '../data/about-me.json';
</script>

<div class="relative mx-16 flex flex-row items-start justify-center gap-16 py-16">
	<!-- left paragraph -->
	<div class="flex flex-3 flex-col items-start justify-start gap-8">
		{#each aboutMe as para}
			<p class="font-body glow text-[18px] text-on-background">
				{@html para.replaceAll('[', '<span class="text-holo-blue">').replaceAll(']', '</span>')}
			</p>
		{/each}
	</div>

	<!-- right skills -->
	<div class="flex flex-1 flex-col items-start justify-start gap-8 rounded-xl bg-holo-blue p-8">
		<!-- skills title -->
		<h1 class="font-title no-selection text-[36px] text-on-primary">Skills</h1>

		<!-- skills list -->
		<ul class="grid w-full grid-cols-2 gap-x-4">
			{#each skills as skill}
				<li class="font-body primary-selection text-[18px] text-on-primary">
					<span class="no-selection">⋄&nbsp</span>{skill}
				</li>
			{/each}
		</ul>
	</div>
</div>
