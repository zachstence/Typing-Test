<script lang="ts">
    import type WordInfo from "./WordInfo";

    export let wordInfo: WordInfo;

    console.log(wordInfo.word, wordInfo.correctCount, wordInfo.mistakeCount);
</script>

<span class="word">
    {#each wordInfo.word as c, i}
        <span class={i < wordInfo.correctCount ? "correct" : i < wordInfo.correctCount + wordInfo.mistakeCount ? "mistake" : ""}>{c}</span>
    {/each}
</span>


<style>
    .word {
        margin-right: 0.25em;
    }

    .correct {
        background-color: limegreen;
    }

    .mistake {
        background-color: red;
    }
</style>