<script>
	const navigations = [
		{
			name: 'Top',
			navigationId: '#top'
		},
		{
			name: 'About Me',
			navigationId: '#about-me'
		},
		{
			name: 'Projects',
			navigationId: '#projects'
		},
		{
			name: 'Contact Me',
			navigationId: '#contact-me'
		}
	];
</script>

<header class="fixed top-0 flex w-full flex-row gap-16 bg-white/65 px-16 py-8">
	{#each navigations as { name, navigationId }}
		<a href={navigationId} class="font-title">{name}</a>
	{/each}
</header>
