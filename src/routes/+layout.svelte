<script>
	import '../app.css';
</script>

<slot />

<style lang="postcss">
	:global(html) {
		background-color: theme(colors.neutral.50);
		padding: theme(padding.2);
	}
</style>
