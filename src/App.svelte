<script lang="ts">
    import Word from "./Word.svelte";
    import type WordInfo from "./WordInfo";
    import random from "./random.json";


    let typed = "";

    const NUM_WORDS = 30;
    const subset = random.sort(() => 0.5 - Math.random()).slice(0, NUM_WORDS);

    let wordInfos: WordInfo[] = subset.map(w => ({
        word: w,
        correctCount: 0,
        mistakeCount: 0
    }));

    let wordIndex = 0;

    let start: Date;
    let wpm = 0;
    let cpm = 0;

    function onInput(e) {
        if (!start) start = new Date();

        const wordInfo = wordInfos[wordIndex];
        if (!wordInfo) return;

        if (e.data === " ") {
            const typedWithoutSpace = typed.substr(0, typed.length - 1);
            if (typedWithoutSpace === wordInfo.word) {
                wordIndex++;
                typed = "";

                // Recalculate WPM/CPM
                const millis = (new Date().getTime() - start.getTime());
                const minutes = millis / 60000;
                wpm = (wordIndex + 1) / minutes
                const chars = wordInfos.reduce((sum, wi) => sum += wi.correctCount, 0);
                cpm = chars / minutes;
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
        <input autofocus bind:value={typed} on:input={onInput} />
        <p>WPM: {wpm}</p>
        <p>CPM: {cpm}</p>
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
