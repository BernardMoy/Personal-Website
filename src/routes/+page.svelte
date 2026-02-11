<script lang="ts">
	import Circle from './Circle.svelte';
	import CircleArrow from './CircleArrow.svelte';
	import Topbar from './Topbar.svelte';
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
			<h2 class="font-main-title text-[36px] text-on-primary">Motivational quote</h2>
		</div>

		<!-- 1 2 3 4 buttons -->
		<div class="absolute top-0 m-4 mt-[96px] flex flex-col gap-4">
			{#each { length: 4 } as _, i}
				<Circle text={(i + 1).toString()} onclick={() => {}}></Circle>
			{/each}
		</div>

		<!-- the 4 rectangles on the top right -->
		<div class="absolute top-0 right-0 mt-[80px] grid grid-cols-2">
			<button class="h-[64px] w-[160px] cursor-pointer bg-primary"></button>
			<button class="h-[64px] w-[160px] bg-on-primary"></button>
			<button class="h-[64px] w-[160px] bg-on-primary"></button>
			<button class="h-[64px] w-[160px] bg-primary"></button>
		</div>
	</div>

	<!-- About me separator -->
	<div class="relative z-10 h-[96px] w-full bg-primary"></div>

	<!-- About me -->
	<div class="relative z-0 h-screen w-full">
		<!-- background image -->
		<!-- this is relative to force the viewport height by the outer wrapper -->
		<div class="absolute bottom-0 w-full">
			<img src="/images/bg-2.png" alt="bg-2" class=" w-full object-cover opacity-45" />
		</div>

		<!-- header-->
		<div class="relative">
			<img
				src="/svgs/header-grid.svg"
				alt="header-grid"
				class="h-[160px] w-full object-cover opacity-40"
			/>
			<p class="font-title absolute top-1/2 left-16 -translate-y-1/2 text-[48px] text-primary">
				About Me
			</p>
			<img
				src="/svgs/code-text.svg"
				alt="code"
				class="absolute top-1/2 right-0 h-[160px] -translate-y-1/2 object-cover"
			/>
		</div>

		<!-- content -->
		<div class="relative mx-16 my-24 flex flex-row items-start justify-center gap-16">
			<!-- left paragraph -->
			<div class="flex flex-3 flex-col items-start justify-start gap-8">
				<p class="font-body text-on-background">
					I graduated with a <span class="text-primary"
						>First Class Honours Bachelor's degree in Computer Science</span
					>
					from the University of Warwick in 2025, and is now studying for a
					<span class="text-primary">Masters of Advanced Computing</span> at Imperial College London.
				</p>
				<p class="font-body text-on-background">
					I am interested in turning creative ideas into software and code, and enjoy constantly
					learning new things. Currently looking for careers in full-stack software development.
				</p>
			</div>

			<!-- right skills -->
			<div
				class="flex flex-1 flex-col items-start justify-start gap-8 rounded-[12px] bg-primary p-8"
			>
				<h1 class="font-title text-[36px] text-on-primary">Skills</h1>
				<p class="font-body text-[18px] text-on-primary">
					Python, Java, Kotlin, HTML, CSS, JavaScript, TypeScript, SQL, React, Git
				</p>
			</div>
		</div>
	</div>

	<!-- Projects -->

	<!-- Contact me -->

	<!-- Ending -->

	<!-- the fixed scroll to next page arrow down button -->
	<div class="fixed bottom-8 flex w-full flex-col items-center">
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
