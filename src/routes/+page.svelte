<script lang="ts">
	import Topbar from './Topbar.svelte';
</script>

<main>
	<!-- the fixed position top navigation bar -->
	<Topbar />

	<img src="/images/bg-1.png" alt="bg-1" class="h-screen w-full object-cover" />
</main>

<!-- reusable component
{#snippet formStep({ question, id, type }: { question: string; id: string; type: string })}
	<article>
		<div>
			<label for={id}>{question}</label>
			<input {type} {id} bind:value={formState[id]} />
		</div>
	</article>
{/snippet} -->
