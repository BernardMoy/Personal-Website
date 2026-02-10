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

<!-- currently it has a fixed height of 80px -->
<header
	class="fixed top-0 z-10 flex h-[80px] w-full flex-row items-center gap-16 bg-white/65 px-16"
>
	{#each navigations as { name, navigationId }}
		<a href={navigationId} class="font-title">{name}</a>
	{/each}
</header>
