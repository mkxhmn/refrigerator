<script lang="ts">
	export let index = 0;
	export let guess: string[] = [];
	export let secret: string[] = [];

	$: validation = validate(guess);

	function validate(guess: string[]) {
		if (!guess?.length) {
			return [];
		}

		const visited: number[] = [];

		const results = guess
			.reduce<string[]>((acc, color, index) => {
				if (color === secret[index]) {
					visited.push(index);
					return acc.concat('hit');
				}

				const missed = secret
					.filter((_, index) => !visited.includes(index))
					.findIndex((secretColor) => secretColor === color);

				// JS will return -1 if the element is not in the array
				if (missed >= 0) {
					visited.push(missed);

					return acc.concat('miss');
				}

				return acc;
			}, [])
			.sort();

		return results;
	}
</script>

<div class="p-2 flex flex-row content-center">
	<span class="flex"># {index + 1}</span>
	{#each validation as result}
		<div
			class="h-4 w-4 flex even:mx-1 rounded-full {result === 'hit' ? 'bg-red-400' : 'bg-gray-400'}"
		/>
	{/each}
</div>
