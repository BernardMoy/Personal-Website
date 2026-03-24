<script lang="ts">
	import FloatingArrowButton from './FloatingArrowButton.svelte';
	import Topbar from './Topbar.svelte';
	import AboutMe from './AboutMe.svelte';
	import Projects from './Projects.svelte';
	import Top from './Top.svelte';
	import ContactMe from './ContactMe.svelte';
	import { onMount } from 'svelte';
	import navigations from '../data/navigations.json';
	import Ending from './Ending.svelte';
	import Loading from './Loading.svelte';
	import { fade, fly } from 'svelte/transition';
	import { asset } from '$app/paths';

	/* whether the page is loading. If yes, the entire screen is filled with a loading wheel */
	let isLoading: boolean = $state(true);

	/*
	Scroll index refers to which part the user has scrolled to: 
	0 = top, 1 = about me, 2 = projects, 3 = contact me (according to the order in navigations.json)
	which is used to control the change of primary colors. 
	Changed when over 50% of the area is scrolled to the next page. 
	*/
	let scrollIndex: number = $state(0);

	onMount(() => {
		// retrieve saved scroll index from browser
		const savedScrollIndex = localStorage.getItem('scrollIndex');
		if (savedScrollIndex) {
			scrollIndex = Number(savedScrollIndex);
		}

		// whenever scroll index changes, update its browser storage value
		$effect(() => {
			localStorage.setItem('scrollIndex', scrollIndex.toString());
		});

		// create observer that detects when the user intersects an element by 50%
		const observerForward = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry, index) => {
					// cast to html element
					const el: HTMLElement = entry.target as HTMLElement;

					// if intersects, change the scroll index to the data-scrollIndex data attribute
					if (entry.isIntersecting) {
						scrollIndex = Number(el.dataset.scrollindex);
					}
				});
			},
			{ rootMargin: '0px 0px -100% 0px', threshold: 0 } // trigger the event when the separator touches the top y of the screen
		);

		const observerBackward = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry, index) => {
					// cast to html element
					const el: HTMLElement = entry.target as HTMLElement;

					// if intersects, change the scroll index to the data-scrollIndex data attribute
					if (entry.isIntersecting) {
						const n = Number(el.dataset.scrollindex);
						if (scrollIndex == n && scrollIndex > 0) {
							// scroll index = n mean the user is scrolling from bottom to top:
							scrollIndex = n - 1;
						}
					}
				});
			},
			{ rootMargin: '-100% 0px 0px 0px', threshold: 0 } // trigger the event when the separator touches the bottom y of the screen
		);

		// observe all separator elements from navigation.json when loading has finished
		$effect(() => {
			if (!isLoading) {
				for (const nav of navigations) {
					const sep = document.getElementById(nav.navigationId);
					if (sep) observerForward.observe(sep);
					if (sep) observerBackward.observe(sep);
					// if (sep) observerSnap.observe(sep);
				}
			}
		});

		// function to be called when everything is loaded
		const handleLoaded = () => {
			isLoading = false;
		};

		// if already loaded, directly call it, else add event listener
		if (document.readyState === 'complete') {
			handleLoaded();
		} else {
			window.addEventListener('load', handleLoaded);
		}

		return () => {
			observerForward.disconnect();
			observerBackward.disconnect();
			// observerSnap.disconnect();

			window.removeEventListener('load', handleLoaded);
		};
	});

	// change the primary color according when the scroll index changes
	// except when the scrollIndex = 0, which is handled in Top.svelte
	$effect(() => {
		if (scrollIndex == 0) return;
		document.documentElement.style.setProperty(
			'--color-primary',
			navigations[scrollIndex]['color']
		);
	});

	// for the floating down / up button click
	function handleFloatingArrowClick() {
		const newIndex: number = (scrollIndex + 1) % navigations.length;
		const element: HTMLElement | null = document.getElementById(navigations[newIndex].navigationId);
		console.log(element);
		element?.scrollIntoView({
			behavior: 'smooth'
		});
	}

	// load time is 400 if first time load, otherwise 0 if refresh
	// for removing the loading screen
	function getLoadOptions() {
		if (document.cookie.indexOf('visited') == -1) {
			document.cookie = 'visited';
			// the delay is intentional, to slow the user down :)
			return { delay: Math.random() * (800 - 400) + 400, duration: 400 };
		} else {
			return { delay: 0, duration: 0 };
		}
	}
</script>

{#if isLoading}
	<main class="fixed z-80" out:fade={getLoadOptions()}>
		<Loading />
	</main>
{:else}
	<main class="bg-main">
		<!-- the fixed position top navigation bar -->
		<Topbar />

		<!-- Top -->
		<section>
			<!-- Top separator -->
			<div id="top" data-scrollindex="0" class="separator"></div>
			<!-- Top (images) content -->
			<Top {scrollIndex} />
		</section>

		<!-- About me -->
		<section>
			<!-- About me separator -->
			<img
				id="about-me"
				data-scrollindex="1"
				class="separator relative z-10 h-[80px] w-full object-cover"
				src={asset('/images/sep-1.png')}
				alt="separation"
			/>

			<div class="relative min-h-screen w-full">
				<!-- background image -->
				<div class="sticky top-0 h-screen w-full">
					<img
						src={asset('/images/bg-2.png')}
						alt="bg-2"
						class="-z-20 h-full w-full object-cover opacity-30"
					/>
				</div>

				<!-- About me content -->
				<div class="relative -mt-[100vh] flex w-full flex-col overflow-x-hidden overflow-y-hidden">
					<!-- header -->
					{@render HeaderAboutMe()}

					<!-- content -->
					<AboutMe />

					<!-- additional deco -->
					<img
						src={asset('/svgs/deco-circle-dot.svg')}
						alt="decoration"
						class="absolute top-12 -left-60 -z-10 scale-75 rotate-90"
					/>
					<img
						src={asset('/svgs/deco-circle-dot.svg')}
						alt="decoration"
						class="absolute -right-48 -bottom-4 -z-10 rotate-260"
					/>
				</div>
			</div>
		</section>

		<!-- projects -->
		<section>
			<!-- Projects separator -->
			<img
				id="projects"
				data-scrollindex="2"
				class="separator relative z-10 h-[80px] w-full object-cover"
				src={asset('/images/sep-2.png')}
				alt="separation"
			/>

			<div class="relative min-h-screen w-full">
				<!-- background image -->
				<div class="sticky top-24 h-screen w-full">
					<img
						src={asset('/images/bg-3.png')}
						alt="bg-3"
						class="-z-20 h-full w-full object-cover opacity-30"
					/>
				</div>

				<!-- projects content -->
				<div class="relative -mt-[100vh] flex w-full flex-col overflow-x-hidden overflow-y-hidden">
					<!-- header -->
					{@render HeaderProjects()}

					<!-- content -->
					<Projects />

					<!-- additional deco -->
					<img
						src={asset('/svgs/deco-lines.svg')}
						alt="decoration"
						class="absolute top-69 -left-32 -z-10 h-[190px] object-cover md:-left-24"
					/>

					<img
						src={asset('/svgs/deco-lines.svg')}
						alt="decoration"
						class="absolute top-24 -right-32 -z-10 h-[220px] rotate-150 object-cover md:-right-24"
					/>
				</div>
			</div>
		</section>

		<!-- contact me -->
		<section>
			<!-- Contact me separator -->
			<img
				id="contact-me"
				data-scrollindex="3"
				class="separator relative z-10 h-[80px] w-full object-cover"
				src={asset('/images/sep-3.png')}
				alt="separation"
			/>

			<div class="relative min-h-[75vh] w-full">
				<!-- background image -->
				<!-- move it down using translate because this part wont scroll normally -->
				<div
					class="sticky top-0 h-[75vh] w-full translate-y-36 overflow-x-hidden overflow-y-hidden"
				>
					<img
						src={asset('/images/bg-4.png')}
						alt="bg-4"
						class="-z-20 h-full w-full object-cover opacity-30"
					/>
				</div>

				<!-- contact me content -->
				<div
					class="relative -mt-[75vh] flex min-h-[75vh] w-full flex-col overflow-x-hidden overflow-y-hidden"
				>
					<!-- header -->
					{@render HeaderContactMe()}

					<!-- content -->
					<ContactMe />

					<!-- additional deco -->
					<img
						src={asset('/svgs/deco-halftone.svg')}
						alt="decoration"
						class="absolute -right-48 -bottom-25 -z-10 h-[310px] object-cover md:-right-36"
					/>
				</div>
			</div>
		</section>

		<!-- Ending -->
		<!-- Add an min height to avoid shrinking too much, causing it to auto scroll back above -->
		<section class="relative w-full">
			<Ending />
		</section>

		<!-- the fixed scroll to next page arrow down button -->
		<div class="no-selection fixed bottom-8 z-50 flex w-full flex-col items-center">
			<FloatingArrowButton scrollindex={scrollIndex} onclick={handleFloatingArrowClick}
			></FloatingArrowButton>
		</div>
	</main>
{/if}

<!-- header components -->
{#snippet HeaderAboutMe()}
	<div class="relative">
		<!-- header image -->
		<img
			src={asset('/svgs/header-grid.svg')}
			alt="header-grid"
			class="h-[160px] w-full object-cover object-left opacity-40"
		/>
		<!-- header title -->
		<h1
			class="font-title glow no-selection absolute top-1/2 left-16 -translate-y-1/2 text-[3rem] text-holo-blue"
		>
			About Me
		</h1>
		<!-- additional deco -->
		<img
			src={asset('/svgs/code-text.svg')}
			alt="decoration"
			class="absolute top-0 -right-55 h-[160px] object-cover sm:-right-35 md:right-0"
		/>
	</div>
{/snippet}

{#snippet HeaderProjects()}
	<div class="relative">
		<!-- header image -->
		<img
			src={asset('/svgs/header-strip.svg')}
			alt="header-strip"
			class="h-[160px] w-full object-cover object-left opacity-40"
		/>
		<!-- header title -->
		<h1
			class="font-title glow no-selection absolute top-1/2 left-16 -translate-y-1/2 text-[3rem] text-holo-pink"
		>
			Projects
		</h1>
	</div>
{/snippet}

{#snippet HeaderContactMe()}
	<div class="relative">
		<!-- header image -->
		<img
			src={asset('/svgs/header-dots.svg')}
			alt="header-dots"
			class="h-[160px] w-full object-cover object-left opacity-65"
		/>
		<!-- header title -->
		<h1
			class="font-title glow no-selection absolute top-1/2 left-16 -translate-y-1/2 text-[3rem] text-holo-orange"
		>
			Contact Me
		</h1>
	</div>
{/snippet}
