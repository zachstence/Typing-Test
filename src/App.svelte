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

    let start: Date;
    let wpm: number;

    function onInput(e) {
        if (!start) start = new Date();

        const wordInfo = wordInfos[wordIndex];
        if (!wordInfo) return;

        if (e.data === " ") {
            const typedWithoutSpace = typed.substr(0, typed.length - 1);
            if (typedWithoutSpace === wordInfo.word) {
                wordIndex++;
                typed = "";

                // Recalculate WPM
                const millis = (new Date().getTime() - start.getTime());
                const minutes = millis / 60000;
                wpm = (wordIndex + 1) / minutes
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
            {#each wordInfos as wordInfo (wordInfo.word)}
                <Word {wordInfo} />
            {/each}
        </div>
        <input bind:value={typed} on:input={onInput} />
        <p>WPM: {wpm}</p>
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
