<!--Rectangular button with sliding hovering effect -->
<!-- Currently fixed to the color of holo pink. Parameterise it, by exlicitly listing out the class instead of parameterise them (classes only generate at runtime)-->
<script lang="ts">
	let {
		text,
		onclick,
		selected = false
	}: { text: string; onclick: () => void; selected: boolean; color: string } = $props();
</script>

<!-- Fixed blue circle right now -->
<!-- use overflow hidden on the root button to clip the sliding background -->
<button
	class="group relative flex w-auto cursor-pointer items-center justify-center border-1 px-4 py-1
	{selected
		? 'border-holo-pink bg-on-primary'
		: `border-on-primary bg-holo-pink`} hover:border-holo-pink"
	{onclick}
>
	<!-- the background hover cover that scales from left to right -->
	<span
		class="absolute z-15 h-full w-full origin-left scale-x-0 bg-on-primary duration-500 ease-in-out group-hover:scale-x-100"
	>
	</span>

	<!-- the text -->
	<div
		class="font-title z-16 text-[1.5rem] {selected
			? 'text-holo-pink'
			: 'text-on-primary'} duration-300 group-hover:text-holo-pink group-active:scale-90"
	>
		{text}
	</div>
</button>
