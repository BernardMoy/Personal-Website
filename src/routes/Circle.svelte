<script lang="ts">
	let { text, onclick, selected }: { text: string; onclick: () => void; selected: boolean } =
		$props();
</script>

<!-- Fixed blue circle right now -->
<!-- use overflow hidden on the root button to clip the sliding background -->
<button
	class="group relative flex h-[48px] w-[48px] cursor-pointer items-center justify-center overflow-hidden rounded-full border-1
	{selected
		? 'border-primary bg-on-primary'
		: 'border-on-primary bg-primary'} hover:border-primary focus:border-primary"
	{onclick}
>
	<!-- the background hover cover that scales from left to right -->
	<span
		class="cover absolute z-15 h-[48px] w-[48px] origin-left scale-x-0 bg-on-primary duration-500 ease-in-out group-hover:scale-x-100 group-focus:scale-x-100"
	>
	</span>

	<!-- the number text -->
	<div
		class="font-title z-16 text-[18px] {selected
			? 'text-primary'
			: 'text-on-primary'} group-hover:text-primary group-focus:text-primary"
	>
		{text}
	</div>
</button>
