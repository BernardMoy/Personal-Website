<script lang="ts">
	import Circle from './Circle.svelte';
	import CircleArrow from './CircleArrow.svelte';
	import Topbar from './Topbar.svelte';
</script>

<main>
	<!-- the fixed position top navigation bar -->
	<Topbar />

	<!-- Main background -->
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

	<p class="font-body text-on-background">
		I graduated with a First Class Honours Bachelor's degree in Computer Science from the University
		of Warwick in 2025, and is now studying for a Masters of Advanced Computing at Imperial College
		London. I am interested in turning creative ideas into software and code, and enjoy constantly
		learning new things. Currently looking for careers in full-stack software development.
	</p>

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
