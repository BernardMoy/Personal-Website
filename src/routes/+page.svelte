<script lang="ts">
	import Circle from './Circle.svelte';
	import CircleArrow from './CircleArrow.svelte';
	import Topbar from './Topbar.svelte';
	import skills from '../data/skills.json';
</script>

<main>
	<!-- the fixed position top navigation bar -->
	<Topbar />

	<!-- Top -->
	<div class="relative text-center">
		<img src="/images/bg-1.png" alt="bg-1" class=" h-screen w-full object-cover" />

		<!-- centered text -->
		<div class="absolute top-1/2 flex w-full -translate-y-1/2 flex-col items-center">
			<h1 class="font-main-title text-[64px] text-on-primary">Hi, I'm Bernard!</h1>
			<h2 class="font-main-title text-[36px] text-on-primary">Welcome :)</h2>
		</div>

		<!-- 1 2 3 4 buttons -->
		<div class="no-selection absolute top-0 m-4 mt-[96px] flex flex-col gap-4">
			{#each { length: 4 } as _, i}
				<Circle text={(i + 1).toString()} onclick={() => {}}></Circle>
			{/each}
		</div>

		<!-- the 4 rectangles on the top right -->
		<div class="no-selection absolute top-0 right-0 mt-[80px] grid grid-cols-2">
			<button class="h-[64px] w-[160px] cursor-pointer bg-holo-blue"></button>
			<button class="h-[64px] w-[160px] bg-on-primary"></button>
			<button class="h-[64px] w-[160px] bg-on-primary"></button>
			<button class="h-[64px] w-[160px] bg-holo-blue"></button>
		</div>
	</div>

	<!-- About me separator -->
	<img
		class="relative z-10 h-[96px] w-full object-cover"
		src="/images/sep-1.png"
		alt="separation"
	/>

	<!-- About me -->
	<div class="relative z-0 min-h-screen w-full">
		<!-- background image -->
		<!-- this is relative to force the viewport height by the outer wrapper -->
		<div class="absolute bottom-0 w-full">
			<img src="/images/bg-2.png" alt="bg-2" class=" min-h-screen w-full object-cover opacity-45" />
		</div>

		<!-- additional deco -->
		<img
			src="/svgs/deco-circle-dot.svg"
			alt="decoration"
			class=" absolute top-12 -left-55 scale-75 rotate-90"
		/>
		<img
			src="/svgs/deco-circle-dot.svg"
			alt="decoration"
			class="absolute -right-48 bottom-4 rotate-260"
		/>

		<!-- header-->
		<div class="relative">
			<!-- header image -->
			<img
				src="/svgs/header-grid.svg"
				alt="header-grid"
				class="h-[160px] w-full object-cover opacity-40"
			/>
			<!-- header title -->
			<p
				class="font-title no-selection absolute top-1/2 left-16 -translate-y-1/2 text-[48px] text-holo-blue"
			>
				About Me
			</p>
			<!-- additional deco -->
			<img
				src="/svgs/code-text.svg"
				alt="code"
				class="absolute top-1/2 right-0 h-[160px] -translate-y-1/2 object-cover"
			/>
		</div>

		<!-- content -->
		<div class="relative mx-16 my-18 flex flex-row items-start justify-center gap-16">
			<!-- left paragraph -->
			<div class="flex flex-3 flex-col items-start justify-start gap-8">
				<p class="font-body text-on-background">
					I graduated with a <span class="text-holo-blue"
						>First Class Honours Bachelor's degree in Computer Science</span
					>
					from the University of Warwick in 2025, and is now studying for a
					<span class="text-holo-blue">Masters of Advanced Computing</span> at Imperial College London.
				</p>
				<p class="font-body text-on-background">
					I am interested in turning creative ideas into software and code, and enjoy constantly
					learning new things. Currently looking for careers in full-stack software development.
				</p>
			</div>

			<!-- right skills -->
			<div
				class="flex flex-1 flex-col items-start justify-start gap-8 rounded-[12px] bg-holo-blue p-8"
			>
				<!-- skills title -->
				<h1 class="font-title holo-blue-selection no-selection text-[36px] text-on-primary">
					Skills
				</h1>

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
	</div>

	<!-- Projects separator -->
	<img
		class="relative z-10 h-[96px] w-full object-cover"
		src="/images/sep-2.png"
		alt="separation"
	/>

	<!-- Projects -->
	<div class="relative z-0 h-screen w-full">
		<!-- background image -->
		<!-- this is relative to force the viewport height by the outer wrapper -->
		<div class="absolute bottom-0 w-full">
			<img src="/images/bg-3.png" alt="bg-3" class=" min-h-screen w-full object-cover opacity-45" />
		</div>

		<!-- additional deco -->

		<!-- header-->
		<div class="relative">
			<!-- header image -->
			<img
				src="/svgs/header-strip.svg"
				alt="header-strip"
				class="h-[160px] w-full object-cover opacity-40"
			/>
			<!-- header title -->
			<p
				class="font-title no-selection absolute top-1/2 left-16 -translate-y-1/2 text-[48px] text-holo-pink"
			>
				Projects
			</p>
			<!-- additional deco -->
		</div>

		<!-- content -->
		<div class="relative mx-16 my-18 flex flex-row items-start justify-center gap-16"></div>
	</div>

	<!-- Contact me separator -->
	<img
		class="relative z-10 h-[96px] w-full object-cover"
		src="/images/sep-3.png"
		alt="separation"
	/>

	<!-- Ending -->

	<!-- the fixed scroll to next page arrow down button -->
	<div class="no-selection fixed bottom-8 z-50 flex w-full flex-col items-center">
		<CircleArrow onclick={() => {}}></CircleArrow>
	</div>
</main>

<!-- reusable component
{#snippet formStep({ question, id, type }: { question: string; id: string; type: string })}
	<article>
		<div>
			<label for={id}>{question}</label>
			<input {type} {id} bind:value={formState[id]} />
		</div>
	</article>
{/snippet} -->
