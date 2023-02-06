<script lang="ts">
	export let guess: string[] = [];
</script>

<div class="grid grid-cols-4 my-4 gap-4 justify-center">
	{#each guess as color}
		<div class="flex justify-center">
			<span
				class="h-16 w-16 rounded-md col-span-1 border-black border-2"
				style="background-color:{color};"
			/>
		</div>
	{/each}
</div>
