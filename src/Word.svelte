<script lang="ts">
    export let word: string;
    export let correct: Boolean[];

    function getClass(i) {
        const c = correct[i];
        if (c === null || c === undefined) return "";
        else if (c) return "green";
        else return "red";
    }
</script>


<style>
    .word {
        margin-right: 0.25em;
    }
    .red {
        color: red;
    }

    .green {
        color: green;
    }
</style>


<span class="word">
{#each word as c, i}
    <span class={getClass(i)}>{c}</span>
    {/each}
</span>