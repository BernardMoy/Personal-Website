<script lang="ts">
	import CircleArrow from './CircleArrow.svelte';
	import Topbar from './Topbar.svelte';
	import AboutMe from './AboutMe.svelte';
	import Projects from './Projects.svelte';
	import Top from './Top.svelte';
</script>

<main>
	<!-- the fixed position top navigation bar -->
	<Topbar />

	<!-- Top -->
	<Top />

	<!-- About me separator -->
	<img
		class="relative z-10 h-[96px] w-full object-cover"
		src="/images/sep-1.png"
		alt="separation"
	/>

	<!-- About me -->
	<section class="relative min-h-screen w-full">
		<!-- background image -->
		<div class="sticky top-0 h-screen w-full">
			<img src="/images/bg-2.png" alt="bg-2" class="h-full w-full object-cover opacity-40" />
		</div>
		<!-- additional deco -->

		<div class="relative -mt-[100vh] flex w-full flex-col">
			<!-- header -->
			<div class="relative">
				<!-- header image -->
				<img
					src="/svgs/header-grid.svg"
					alt="header-grid"
					class="h-[160px] w-full object-cover opacity-40"
				/>
				<!-- header title -->
				<h1
					class="font-title no-selection absolute top-1/2 left-16 -translate-y-1/2 text-[48px] text-holo-blue"
				>
					About Me
				</h1>
			</div>

			<!-- content -->
			<AboutMe />
		</div>
	</section>

	<!-- Projects separator -->
	<img
		class="relative z-10 h-[96px] w-full object-cover"
		src="/images/sep-2.png"
		alt="separation"
	/>

	<!-- Projects -->
	<section class="relative min-h-screen w-full">
		<!-- background image -->
		<div class="sticky top-24 h-screen w-full">
			<img src="/images/bg-3.png" alt="bg-3" class="h-full w-full object-cover opacity-40" />
		</div>
		<!-- additional deco -->

		<div class="relative -mt-[100vh] flex w-full flex-col">
			<!-- header -->
			<div class="relative">
				<!-- header image -->
				<img
					src="/svgs/header-strip.svg"
					alt="header-strip"
					class="h-[160px] w-full object-cover opacity-40"
				/>
				<!-- header title -->
				<h1
					class="font-title no-selection absolute top-1/2 left-16 -translate-y-1/2 text-[48px] text-holo-pink"
				>
					Projects
				</h1>
			</div>

			<!-- content -->
			<Projects />
		</div>
	</section>

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
