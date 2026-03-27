<!-- Content of the about me section -->
<script>
	import skills from '../data/skills.json';
	import aboutMe from '../data/about-me.json';
	import FadeIn from './FadeIn.svelte';
</script>

<!-- Gap 16 here is an exception compared to other pages, because it looks less crowded -->
<div
	class="relative z-2 mx-8 flex flex-col items-start justify-center gap-16 py-8 sm:mx-16 sm:gap-16 sm:py-16 md:flex-row"
>
	<!-- left paragraph -->
	<FadeIn delay={500}>
		<div class="flex flex-1 flex-col items-start justify-start gap-8 lg:flex-3">
			{#each aboutMe as para}
				<p class="font-body glow text-[1rem] text-on-background">
					{@html para.replaceAll('[', '<span class="text-holo-blue">').replaceAll(']', '</span>')}
				</p>
			{/each}
		</div>
	</FadeIn>

	<!-- right skills -->
	<FadeIn delay={800}>
		<div
			class="flex w-full flex-1 flex-col items-start justify-start gap-8 rounded-xl bg-holo-blue p-8"
		>
			<!-- skills title -->
			<h1 class="font-title no-selection text-[36px] text-on-primary">Skills</h1>

			<!-- skills list -->
			<ul class="grid w-full grid-cols-2 gap-x-4">
				{#each skills as skill}
					<li class="font-body primary-selection text-[1rem] text-on-primary">
						<span class="no-selection">⋄&nbsp</span>{skill}
					</li>
				{/each}
			</ul>
		</div>
	</FadeIn>
</div>
