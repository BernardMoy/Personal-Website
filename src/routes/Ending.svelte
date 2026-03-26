<!-- Content of ending section -->
<script lang="ts">
	import { onMount } from 'svelte';
	import { asset } from '$app/paths';

	onMount(() => {
		let observer = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					if (entry.isIntersecting) {
						setTimeout(() => {
							entry.target.classList.remove('scale-110');
							entry.target.classList.add('scale-100');
						}, 250);

						observer.disconnect();
					}
				});
			},
			{ threshold: 0.3 }
		);

		// on initial load, scale the ending image from 1.2 to 1.0
		const endingImage = document.getElementById('ending-image');
		if (endingImage) {
			observer.observe(endingImage);
		}

		return () => observer.disconnect();
	});
</script>

<div class="z-2 w-full overflow-hidden">
	<img
		src={asset('/images/bg-5.png')}
		alt="bg-5"
		id="ending-image"
		class="-z-8 min-h-[75vh] w-full scale-110 object-cover duration-1200 ease-out"
	/>
</div>
