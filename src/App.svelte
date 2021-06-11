<script lang="ts">
    import Word from "./Word.svelte";
    import type WordInfo from "./WordInfo";

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
        "direction",
    ];

    let typed = "";

    let wordInfos: WordInfo[] = words.map(w => ({
        word: w,
        correctCount: 0,
        mistakeCount: 0
    }));

    let wordIndex = 0;

    function onInput(e) {
        const wordInfo = wordInfos[wordIndex];

        if (e.data === " ") {
            const typedWithoutSpace = typed.substr(0, typed.length - 1);
            if (typedWithoutSpace === wordInfo.word) {
                wordIndex++;
                typed = "";
            }
            else wordInfo.mistakeCount++;
        } else {
            wordInfo.correctCount = 0;
            wordInfo.mistakeCount = 0;
            for (let i = 0; i < typed.length; i++) {
                if (i < wordInfo.word.length
                        && wordInfo.word[i] === typed[i]
                        && !wordInfo.mistakeCount) {
                    wordInfo.correctCount++;
                } else {
                    wordInfo.mistakeCount++;
                }
            }
        }

        wordInfos = wordInfos;
    }
</script>


<main>
    <div class="wrapper">
        <div class="words">
            {#each wordInfos as wordInfo}
                <Word {wordInfo} />
            {/each}
        </div>
        <input bind:value={typed} on:input={onInput} />
        <p>Typed: {typed}</p>
    </div>
</main>


<style>
    main {
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .wrapper {
        width: 50%;
    }

    .words {
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
    }
</style>
