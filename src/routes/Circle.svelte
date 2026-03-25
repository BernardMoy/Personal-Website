<!--Circular button with sliding hovering effect -->
<script lang="ts">
	let {
		text,
		onclick,
		selected = false,
		color = 'primary'
	}: { text: string; onclick: () => void; selected: boolean; color?: string } = $props();

	// tailwind classes need to be constructed fully, not partially
	let bgColor = $derived('bg-' + color);
	let borderColor = $derived('border-' + color);
	let textColor = $derived('text-' + color);
</script>

<!-- Fixed blue circle right now -->
<!-- use overflow hidden on the root button to clip the sliding background -->
<button
	class="group relative flex h-12 w-12 cursor-pointer items-center justify-center overflow-hidden rounded-full border
    hover:{borderColor} 
    {selected ? `${borderColor} bg-on-primary` : `border-on-primary ${bgColor}`}"
	{onclick}
>
	<!-- the background hover cover that scales from left to right -->
	<span
		class="absolute z-15 h-[48px] w-[48px] origin-left scale-x-0 bg-on-primary duration-500 ease-in-out group-hover:scale-x-100"
	>
	</span>

	<!-- the number text -->
	<div
		class="font-title z-16 text-[1.2rem] {selected
			? `${textColor}`
			: 'text-on-primary'} duration-300 group-hover:{textColor} group-active:scale-80"
	>
		{text}
	</div>
</button>
