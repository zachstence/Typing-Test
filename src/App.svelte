<script lang="ts">
	import Word from "./Word.svelte";

	let words = [
		"bother",
		"elephant",
		"panel",
		"disability",
		"inch",
		"pyramid",
		"separate",
		"nationalism",
		"live",
		"rush",
		"disappointment",
		"salt",
		"file",
		"substitute",
		"green",
		"assignment",
		"garage",
		"horse",
		"default",
		"favorable",
		"penetrate",
		"version",
		"velvet",
		"allocation",
		"pleasure",
		"testify",
		"touch",
		"functional",
		"Koran",
		"direction"
	];
	let typed = "";
	let t = 0;
	
	function onInput(e) {
		console.log(e);
		const toType = words[t];
		
		if (e.data === " ") {
			const word = typed.trim();
			typed = "";
			if (word === toType) {
				console.log(word);
				t++;
			} else {
				console.log("mistake");
			}
		}
	}
</script>


<style>

</style>


{#each words as word}
	<Word word={word} correct={[]} />
{/each}
<input bind:value={typed} on:input={onInput}>
<p>Typed: {typed}</p>

