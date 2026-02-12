<script>
	import skills from '../data/skills.json';
</script>

<div class="relative mx-16 flex flex-row items-start justify-center gap-16 py-16">
	<!-- left paragraph -->
	<div class="flex flex-3 flex-col items-start justify-start gap-8">
		<p class="font-body text-[18px] text-on-background">
			I graduated with a <span class="text-holo-blue"
				>First Class Honours Bachelor's degree in Computer Science</span
			>
			from the University of Warwick in 2025, and is now studying for a
			<span class="text-holo-blue">Masters of Advanced Computing</span> at Imperial College London.
		</p>
		<p class="font-body text-[18px] text-on-background">
			I am interested in turning creative ideas into software and code, and enjoy constantly
			learning new things. Currently looking for careers in full-stack software development.
		</p>
	</div>

	<!-- right skills -->
	<div class="flex flex-1 flex-col items-start justify-start gap-8 rounded-xl bg-holo-blue p-8">
		<!-- skills title -->
		<h1 class="font-title holo-blue-selection no-selection text-[36px] text-on-primary">Skills</h1>

		<!-- skills list -->
		<ul class="grid w-full grid-cols-2 gap-x-4">
			{#each skills as skill}
				<li class="font-body holo-blue-selection text-[18px] text-on-primary">
					<span class="no-selection">⋄&nbsp</span>{skill}
				</li>
			{/each}
		</ul>
	</div>
</div>
