<script context="module" lang="ts">
	export type ColorProps =
		| 'black'
		| 'red'
		| 'green'
		| 'yellow'
		| 'blue'
		| 'magenta'
		| 'cyan'
		| 'white';
</script>

<script lang="ts">
	export let color: ColorProps;
</script>

<span
	class="h-16 w-16 rounded-md col-span-1 border-black border-2"
	style="background-color:{color};"
/>
