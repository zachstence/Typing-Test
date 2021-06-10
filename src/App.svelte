<script lang="ts">
    import Word from "./Word.svelte";

    const keys = {
        BACKSPACE: 8,

    }

    console.log("start");

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
    let token = "";

    let wordIndex = 0;
    let letterIndex = 0;
    let mistakeIndex = 0;

    function onInput(e) {

        console.log(e);

        const word = words[wordIndex];

        if (e.data === " ") {
            const tokenWithoutSpace = token.substr(0, token.length - 1);
            if (tokenWithoutSpace === word) {
                wordIndex++;
                letterIndex = 0;
                token = "";
            }
            else mistakeIndex++;
        } else {
            letterIndex = 0;
            mistakeIndex = 0;
            for (let i = 0; i < token.length; i++) {
                if (word[i] && word[i] === token[i]) {
                    letterIndex++;
                } else {
                    mistakeIndex++;
                }
            }
        }

        console.log(wordIndex, letterIndex, mistakeIndex);

    }
</script>

<main>
    <div class="wrapper">
        <div class="words">
            {#each words as word}
                <Word {word} correct={[]} />
            {/each}
        </div>
        <input bind:value={token} on:input={onInput} />
        <p>Typed: {token}</p>
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
