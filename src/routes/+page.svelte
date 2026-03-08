<script lang="ts">
	import CircleArrow from './CircleArrow.svelte';
	import Topbar from './Topbar.svelte';
	import AboutMe from './AboutMe.svelte';
	import Projects from './Projects.svelte';
	import Top from './Top.svelte';
	import ContactMe from './ContactMe.svelte';
</script>

<main>
	<!-- the fixed position top navigation bar -->
	<Topbar />

	<!-- Top -->
	<Top />

	<!-- About me separator -->
	<img
		id="about-me"
		class="relative z-10 h-[80px] w-full object-cover"
		src="/images/sep-1.png"
		alt="separation"
	/>

	<!-- About me -->
	<section class="relative min-h-screen w-full">
		<!-- background image -->
		<div class="sticky top-0 h-screen w-full">
			<img src="/images/bg-2.png" alt="bg-2" class="-z-20 h-full w-full object-cover opacity-40" />
		</div>
		<!-- additional deco -->

		<div class="relative -mt-[100vh] flex w-full flex-col overflow-x-hidden overflow-y-hidden">
			<!-- header -->
			{@render HeaderAboutMe()}

			<!-- content -->
			<AboutMe />

			<!-- additional deco -->
			<img
				src="/svgs/deco-circle-dot.svg"
				alt="decoration"
				class="absolute top-12 -left-55 -z-10 scale-75 rotate-90"
			/>
			<img
				src="/svgs/deco-circle-dot.svg"
				alt="decoration"
				class="absolute -right-48 -bottom-4 -z-10 rotate-260"
			/>
		</div>
	</section>

	<!-- Projects separator -->
	<img
		id="projects"
		class="relative z-10 h-[80px] w-full object-cover"
		src="/images/sep-2.png"
		alt="separation"
	/>

	<!-- Projects -->
	<section class="relative min-h-screen w-full">
		<!-- background image -->
		<div class="sticky top-24 h-screen w-full">
			<img src="/images/bg-3.png" alt="bg-3" class="-z-20 h-full w-full object-cover opacity-40" />
		</div>
		<!-- additional deco -->

		<div class="relative -mt-[100vh] flex w-full flex-col overflow-x-hidden overflow-y-hidden">
			<!-- header -->
			{@render HeaderProjects()}

			<!-- content -->
			<Projects />

			<!-- additional deco -->
			<img
				src="/svgs/deco-lines.svg"
				alt="decoration"
				class="absolute top-69 -left-24 -z-10 h-[190px] object-cover"
			/>

			<img
				src="/svgs/deco-lines.svg"
				alt="decoration"
				class="absolute top-24 -right-24 -z-10 h-[220px] rotate-150 object-cover"
			/>
		</div>
	</section>

	<!-- Contact me separator -->
	<img
		id="contact-me"
		class="relative z-10 h-[80px] w-full object-cover"
		src="/images/sep-3.png"
		alt="separation"
	/>

	<!-- Contact me -->
	<section class="relative min-h-[75vh] w-full">
		<!-- background image -->
		<!-- move it down using translate because this part wont scroll normally -->
		<div class="sticky top-0 h-[75vh] w-full translate-y-36 overflow-x-hidden overflow-y-hidden">
			<img src="/images/bg-4.png" alt="bg-4" class="-z-20 h-full w-full object-cover opacity-40" />

			<!-- additional deco -->
			<!-- need to stick with background because this is going to the bottom -->
			<!-- this is different from above because normally the background wont stick here -->
			<img
				src="/svgs/deco-halftone.svg"
				alt="decoration"
				class="absolute -right-13 bottom-9 -z-10 h-[310px] object-cover"
			/>
		</div>

		<div class="relative -mt-[75vh] flex w-full flex-col">
			<!-- header -->
			{@render HeaderContactMe()}

			<!-- content -->
			<ContactMe />
		</div>
	</section>

	<!-- Ending -->
	<section class="relative w-full">
		<img src="/images/bg-5.png" alt="bg-5" class="-z-8 w-full object-cover" />
	</section>

	<!-- the fixed scroll to next page arrow down button -->
	<div class="no-selection fixed bottom-8 z-50 flex w-full flex-col items-center">
		<CircleArrow onclick={() => {}}></CircleArrow>
	</div>
</main>

<!-- header components -->
{#snippet HeaderAboutMe()}
	<div class="relative">
		<!-- header image -->
		<img
			src="/svgs/header-grid.svg"
			alt="header-grid"
			class="h-[160px] w-full object-cover opacity-40"
		/>
		<!-- header title -->
		<h1
			class="font-title glow no-selection absolute top-1/2 left-16 -translate-y-1/2 text-[48px] text-holo-blue"
		>
			About Me
		</h1>
		<!-- additional deco -->
		<img
			src="/svgs/code-text.svg"
			alt="decoration"
			class="absolute top-0 right-0 h-[160px] object-cover"
		/>
	</div>
{/snippet}

{#snippet HeaderProjects()}
	<div class="relative">
		<!-- header image -->
		<img
			src="/svgs/header-strip.svg"
			alt="header-strip"
			class="h-[160px] w-full object-cover opacity-40"
		/>
		<!-- header title -->
		<h1
			class="font-title glow no-selection absolute top-1/2 left-16 -translate-y-1/2 text-[48px] text-holo-pink"
		>
			Projects
		</h1>
	</div>
{/snippet}

{#snippet HeaderContactMe()}
	<div class="relative">
		<!-- header image -->
		<img
			src="/svgs/header-dots.svg"
			alt="header-dots"
			class="h-[160px] w-full object-cover opacity-65"
		/>
		<!-- header title -->
		<h1
			class="font-title glow no-selection absolute top-1/2 left-16 -translate-y-1/2 text-[48px] text-holo-orange"
		>
			Contact Me
		</h1>
	</div>
{/snippet}
