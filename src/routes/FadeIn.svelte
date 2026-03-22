<script lang="ts">
	import { type Snippet } from 'svelte';

	let {
		delay,
		children,
		translate = true
	}: { delay: number; children: Snippet; translate?: boolean } = $props();

	// state to handle whether the element is visible on the screen
	let visible = $state(false);

	// bind this function to the fade in wrapper
	function fadeIn(node: HTMLElement) {
		let observer = new IntersectionObserver((entries) => {
			entries.forEach((entry) => {
				if (entry.isIntersecting) {
					setTimeout(() => {
						// change the visible state which adds the loaded class to the fade in wrapper
						visible = true;

						// disconnect the observer, we only need it to run once
						observer.disconnect();
					}, delay);
				}
			});
		});

		// As node does not exist in the DOM tree, it detects visibility change of the first element child
		if (node.firstElementChild) {
			observer.observe(node.firstElementChild);
		}

		return {
			destroy() {
				observer.disconnect();
			}
		};
	}
</script>

<!-- Fade in wrapper decoration, renders conetents only to avoid breaking layouts -->
<div class="fadeinwrapper" class:translate class:loaded={visible} use:fadeIn>
	{@render children()}
</div>

<style>
	/* Make the extra div element (above) disappear from the DOM tree, to avoid affecting the layout */
	.fadeinwrapper {
		display: contents;
	}

	/* Specifies the initial styles before the elements are loaded */
	.fadeinwrapper :global(> *) {
		opacity: 0;
		transition: opacity 0.9s ease-out;
	}

	.fadeinwrapper.translate :global(> *) {
		transform: translateY(10px);
		transition:   /* Overwrites the one above */
			opacity 0.9s ease-out,
			transform 0.9s;
	}

	/* Specifies the styles after the elements are loaded */
	.fadeinwrapper.loaded :global(> *) {
		opacity: 1;
	}

	.fadeinwrapper.translate.loaded :global(> *) {
		transform: translateY(0);
	}
</style>
