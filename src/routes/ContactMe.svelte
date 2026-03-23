<script>
	import contacts from '../data/contacts.json';
</script>

<div class="mx-12 flex flex-col gap-16 py-16 md:mx-16">
	<!-- the row of contact sources -->
	<div class="flex w-full flex-col items-center justify-around gap-16 lg:flex-row lg:gap-0">
		{#each contacts as contact}
			<a
				href={contact.link}
				target="_blank"
				class="group flex flex-row items-center justify-center gap-4 duration-200 ease-out hover:-translate-y-1"
			>
				<svg
					class="shrink-0"
					viewBox="0 0 {contact.w} {contact.h}"
					width={contact.w}
					height={contact.h}
					preserveAspectRatio="xMidYMid meet"
					><path fill="var(--color-on-background)" d={contact.svgData} class="svg-icon" /></svg
				>

				<p class="font-body glow text-[1.5rem] text-on-background">
					<span class="contact-text">
						{contact.text}
					</span>
				</p>
			</a>
		{/each}
	</div>
</div>

<style>
	.contact-text {
		box-decoration-break: clone;
		background: linear-gradient(to right, var(--color-holo-orange), var(--color-holo-orange));

		background-size: 0% 0.1em;
		background-position: 50% 100%; /* grow from the center horizontally */
		background-repeat: no-repeat;

		transition:
			background-size 250ms ease-out,
			color 250ms ease-out;
	}

	.group:hover .contact-text,
	.group:focus .contact-text {
		background-size: 100% 0.1em;
		color: var(--color-holo-orange);
	}

	.svg-icon {
		transition: fill 250ms ease-out;
	}

	.group:hover .svg-icon,
	.group:focus .svg-icon {
		fill: var(--color-holo-orange);
	}
</style>
