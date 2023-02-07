<script lang="ts">
	import ColorBox, { type ColorProps } from './ColorBox.svelte';

	export let guess: ColorProps[] = [];
</script>

<div class="grid grid-cols-4 my-4 gap-4 justify-center">
	{#each guess as color}
		<div class="flex justify-center">
			<ColorBox {color} />
		</div>
	{/each}
</div>
