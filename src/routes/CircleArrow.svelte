<script lang="ts">
	let { onclick }: { onclick: () => void } = $props();
</script>

<button
	class="flex h-[48px] w-[48px] cursor-pointer items-center justify-center rounded-full bg-primary"
	aria-label="next page"
	{onclick}
>
	<img src="/svgs/arrow-down.svg" alt="arrow down" />
</button>
