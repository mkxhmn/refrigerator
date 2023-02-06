<script>
	import '../app.css';
</script>

<h1 class="text-6xl font-bold mt-4 px-8">Mastermind?</h1>

<slot />

<style lang="postcss">
	:global(html) {
		background-color: theme(colors.neutral.50);
		padding: theme(padding.2);
	}
</style>
