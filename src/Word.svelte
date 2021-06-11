<script lang="ts">
    export let word: string;
    export let correct: number;
    export let mistake: number;

    console.log(word, correct, mistake);

    function getClass(i) {
        console.log(`getClass(${i})`);
        if (i < correct) return "correct";
        else if (i < correct + mistake) return "mistake";
        else return "";
    }
</script>

<span class="word">
    {#each word as c, i}
        <span class={i < correct ? "correct" : i < correct + mistake ? "mistake" : ""}>{c}</span>
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