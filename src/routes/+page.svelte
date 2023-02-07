<script lang="ts">
	import Validation from '$lib/Guess.Validation.svelte';
	import Guess from '$lib/Guess.svelte';
	import type { ColorProps } from '$lib/ColorBox.svelte';
	import ColorBox from '$lib/ColorBox.svelte';

	const codePegs: ColorProps[] = [
		'black',
		'red',
		'green',
		'yellow',
		'blue',
		'magenta',
		'cyan',
		'white'
	];

	let inputs: ColorProps[] = ['magenta', 'magenta', 'magenta', 'magenta'];

	const secret: ColorProps[] = ['magenta', 'yellow', 'cyan', 'black'];
	let guesses: ColorProps[][] = [];

	const handleSelect = (e: Event, index: number) => {
		if (e.target instanceof HTMLSelectElement) {
			inputs[index] = e.target.value as ColorProps;
		}
	};

	const handleSubmit = () => {
		// perform a shallow copy to guesses
		guesses.push(inputs.slice());
		guesses = guesses;
	};
</script>

<div id="container">
	<div class="grid grid-cols-2 m-8 mt-4 h-full rounded-xl overflow-hidden border-black border-2">
		<div class="bg-red-50 px-8 flex flex-col content-center justify-center">
			<div class="grid grid-cols-4 gap-4">
				{#each inputs as input, index}
					<div class="grid grid-rows-2 gap-2">
						<ColorBox color={input} />
						<select
							id={input}
							value={input}
							on:change={(e) => handleSelect(e, index)}
							name="selection"
						>
							{#each codePegs as peg}
								<option value={peg}>{peg}</option>
							{/each}
						</select>
					</div>
				{/each}
			</div>
			<button
				class="py-4 w-full border-b-8 transition-all ease-out duration-200 hover:border-b-2 text-center mt-6 bg-neutral-300 rounded-full uppercase text-lg font-bold border-2 border-black"
				on:click={handleSubmit}>submit</button
			>
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
