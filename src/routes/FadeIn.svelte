<script lang="ts">
	import { type Snippet } from 'svelte';

	let {
		delay,
		children,
		effect = 'translate'
	}: { delay: number; children: Snippet; effect?: 'none' | 'translate' | 'zoom' } = $props();

	// state to handle whether the element is visible on the screen
	let visible = $state(false);

	// bind this function to the fade in wrapper div element (below)
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
<div
	class="fadeinwrapper"
	class:translate={effect == 'translate'}
	class:zoom={effect == 'zoom'}
	class:loaded={visible}
	use:fadeIn
>
	{@render children()}
</div>

<style>
	/* Make the extra div element (above) disappear from the DOM tree, to avoid affecting the layout */
	/* Therefore all effects are targetting towards its child > * */
	.fadeinwrapper {
		display: contents;
	}

	/* Specifies the initial styles before the elements are loaded */
	.fadeinwrapper :global(> *) {
		opacity: 0;
		transition:
			opacity 0.9s ease-out,
			transform 1s;
	}

	.fadeinwrapper.translate :global(> *) {
		transform: translateY(10px);
	}

	.fadeinwrapper.zoom :global(> *) {
		transform: scale(1.05);
		transition:
			opacity 0.9s ease-out,
			transform 1.5s ease-out; /* Give zoom effect a longer transform time */
	}

	/* Specifies the styles after the elements are loaded */
	.fadeinwrapper.loaded :global(> *) {
		opacity: 1;
	}

	.fadeinwrapper.translate.loaded :global(> *) {
		transform: translateY(0);
	}

	.fadeinwrapper.zoom.loaded :global(> *) {
		transform: scale(1);
	}
</style>
