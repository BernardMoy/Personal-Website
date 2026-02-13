<script>
	import contacts from '../data/contacts.json';
</script>

<div class="mx-16 flex flex-col gap-16 py-16">
	<!-- the row of contact sources -->
	<div class="flex w-full flex-row items-center justify-around">
		{#each contacts as contact}
			<a
				href={contact.link}
				target="_blank"
				class="flex flex-row items-center justify-center gap-4"
			>
				<img src={contact.image} alt="contact logo" class="h-[64px] w-[64px]" />
				<p class="font-body text-[24px] text-on-background">
					{contact.text}
				</p>
			</a>
		{/each}
	</div>
</div>
