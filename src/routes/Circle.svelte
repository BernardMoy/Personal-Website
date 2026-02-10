<script lang="ts">
	let { text, onclick }: { text: string; onclick: () => void } = $props();
</script>

<button
	class="flex h-[48px] w-[48px] cursor-pointer items-center justify-center rounded-full bg-primary"
	{onclick}
>
	<div class="font-title text-[18px] text-on-primary">
		{text}
	</div>
</button>
