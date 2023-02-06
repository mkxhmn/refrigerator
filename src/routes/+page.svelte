<script lang="ts">
	import Validation from '$lib/Validation.svelte';
	import Guess from '../lib/Guess.svelte';

	const codePegs = ['magenta', 'orange', 'blue', 'purple', 'yellow', 'white', 'green', 'black'];

	const inputs = ['first', 'second', 'third', 'fourth'];

	const secret = ['magenta', 'yellow', 'purple', 'black'];
	let guesses: string[][] = [];

	const handleSubmit = (e: Event) => {
		if (e.target instanceof HTMLFormElement) {
			const form = new FormData(e.target);

			guesses.push(form.getAll('selection') as string[]);

			// currently i am not sure if this is a best way to handle reactivity for array
			guesses = guesses;
		}
	};
</script>

<div id="container">
	<div class="grid grid-cols-2 m-8 mt-4 h-full rounded-xl overflow-hidden border-black border-2">
		<div class="bg-red-50 px-8 flex flex-col content-center justify-center">
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
					class="py-4 w-full border-b-8 transition-all ease-out duration-200 hover:border-b-2 text-center mt-6 bg-neutral-300 rounded-full uppercase text-lg font-bold border-2 border-black"
					type="submit">submit</button
				>
			</form>
		</div>
		<div class="bg-purple-50 p-8 overflow-y-scroll rounded-tr-xl rounded-br-xl">
			{#each guesses as guess, index (index)}
				<div class="border-black bg-white rounded-md border-2 mb-8">
					<Validation {guess} {secret} {index} />
					<Guess {guess} />
				</div>
			{/each}
		</div>
	</div>
</div>

<style lang="postcss">
	div#container {
		height: calc(theme(height.screen) - theme(height.32));
	}
</style>
