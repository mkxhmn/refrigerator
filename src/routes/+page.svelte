<script lang="ts">
	const codePegs = ['magenta', 'orange', 'blue', 'purple', 'yellow', 'white', 'green', 'black'];

	const inputs = ['first', 'second', 'third', 'fourth'];

	const secret = ['magenta', 'yellow', 'purple', 'black'];
	let guesses: string[][] = [];

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

	const handleSubmit = (e: Event) => {
		if (e.target instanceof HTMLFormElement) {
			const form = new FormData(e.target);

			guesses.push(form.getAll('selection') as string[]);

			// currently i am not sure if this is a best way to handle reactivity for array
			guesses = guesses;
		}
	};
</script>

<div>
	<div class="grid grid-cols-2 gap-4 h-screen">
		<div class="bg-red-50 px-8 flex flex-col content-center justify-center">
			<h1 class="text-6xl font-bold mb-8">Mastermind?</h1>
			<form on:submit|preventDefault={handleSubmit}>
				<div class="grid grid-cols-4 gap-4">
					{#each inputs as input}
						<select id={input} name="selection">
							{#each codePegs as peg}
								<option value={peg}>{peg}</option>
							{/each}
						</select>
					{/each}
				</div>
				<button
					class="py-2 w-full text-center mt-6 bg-neutral-300 rounded-md uppercase text-xl font-medium"
					type="submit">submit</button
				>
			</form>
		</div>
		<div class="bg-purple-50">
			{#each guesses as guess, index (index)}
				{@const validation = validate(guess)}
				<div class="border-black bg-white rounded-md border-2 mb-8">
					<div class="p-2 flex flex-row content-center">
						<span class="flex"># {index + 1}</span>
						{#each validation as result}
							<div
								class="h-4 w-4 flex even:mx-1 rounded-full {result === 'hit'
									? 'bg-red-400'
									: 'bg-gray-400'}"
							/>
						{/each}
					</div>
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
				</div>
			{/each}
		</div>
	</div>
</div>
