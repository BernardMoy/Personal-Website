<script>
	import Circle from './Circle.svelte';
	import top from '../data/top.json';

	const backgrounds = [
		{
			name: 'bg-1',
			url: '/images/bg-1-1.png'
		},
		{
			name: 'bg-2',
			url: '/images/bg-1-2.png'
		},
		{
			name: 'bg-3',
			url: '/images/bg-1-3.png'
		},
		{
			name: 'bg-4',
			url: '/images/bg-1-4.png'
		}
	];
</script>

<div class="relative text-center">
	<img src="/images/bg-1-1.png" alt="bg-1" class=" h-screen w-full object-cover" />

	<!-- centered text -->
	<div class="absolute top-1/2 flex w-full -translate-y-1/2 flex-col items-center">
		<h1 class="font-main-title text-[64px] text-on-primary">{top.title}</h1>
		<h2 class="font-main-title text-[36px] text-on-primary">{top.subtitle}</h2>
	</div>

	<!-- 1 2 3 4 buttons -->
	<div class="no-selection absolute top-0 m-4 mt-[96px] flex flex-col gap-4">
		{#each { length: 4 } as _, i}
			<Circle text={(i + 1).toString()} onclick={() => {}}></Circle>
		{/each}
	</div>

	<!-- the 4 rectangles on the top right -->
	<div class="absolute top-0 right-0 mt-[80px] flex flex-col">
		<div class="no-selection grid grid-cols-2">
			{#each backgrounds as bg}
				<button
					aria-label={bg.name}
					class="h-[64px] w-[160px] cursor-pointer bg-cover bg-center"
					style={`background-image: url(${bg.url})`}
				></button>
			{/each}
		</div>

		<!-- Progress bar -->
		<div class="no-selection h-1 w-full bg-on-primary"></div>
	</div>
</div>
