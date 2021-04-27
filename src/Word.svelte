<script lang="ts">
    export let word: string;
    export let correct: Boolean[];
</script>


<style>

</style>


{#each word as c, i}
    <span class={correct[i] ? "green" : "red"}>{c}</span>
{/each}