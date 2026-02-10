<script lang="ts">
	import Topbar from './Topbar.svelte';
</script>

<main>
	<!-- the fixed position top navigation bar -->
	<Topbar />

	<img src="/images/bg-1.png" alt="bg-1" class="h-screen w-full object-cover" />

	<div class="font-main-title">Hi I'm Bernard</div>

	<p class="font-body">
		I graduated with a First Class Honours Bachelor's degree in Computer Science from the University
		of Warwick in 2025, and is now studying for a Masters of Advanced Computing at Imperial College
		London. I am interested in turning creative ideas into software and code, and enjoy constantly
		learning new things. Currently looking for careers in full-stack software development.
	</p>
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
