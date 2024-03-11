<script>
    import { fade } from "svelte-transitions";

    export let page = 0;
    export const lastPage = 6;

    function nextPage() {
        page += 1;
        console.log(page)
    }

    function previousPage() {
        page -= 1;
    }

    function skipToEnd() {
        page = lastPage;
    }
</script>

<div id="narrative" in:fade={{ duration: 500 }} out:fade={{ duration: 500, css: (t) => `opacity: ${t*0}` }}>
    <div class="text">
        <p class="page-num">{page} / {lastPage}</p>
        <button class="previous {page === 0 ? 'disabled' : ''}" on:click={previousPage} disabled={page === 0}>Previous</button>
        <button class="next {page === lastPage ? 'disabled' : ''}" on:click={nextPage} disabled={page === lastPage}>Next</button>
        <button class="skip {page === lastPage ? 'disabled' : ''}" on:click={skipToEnd} disabled={page === lastPage}>Skip to end</button>
    </div>
</div>

<style>
    #narrative {
        font-family: Helvetica;
        font-size: 0.9em;
        height: 940px;
        width: 100%;
        background-color: rgba(255,255,255, 1);
    }

    .text {
        display: flex;
        flex-wrap: wrap;
        background-color: lightgray;
        padding: 20px;
        height: 23.5%;
        position: relative;
    }

    button {
        font-size: 1.2em;
        color: rgba(95, 95, 95, 1);
        background-color: rgba(58, 58, 58, 0);
        border: 2px solid rgba(51, 51, 51, 0.3);
        border-radius: 5px;
        text-decoration: underline dotted;
        font-style: italic;
        padding: 10px;
        margin: 0px 10px;
        z-index: 0;
        position: absolute;
    }

    button[disabled] {
        opacity: 0.4;
        cursor: not-allowed;
    }

    button:hover {
        color: rgba(58, 58, 58, 0.5);
    }

    .previous {
        right: 250px;
        bottom: 20px;
        background-color: lightcoral;
    }
    .next {
        right: 180px;
        bottom: 20px;
        background-color: lightgreen;
    }
    .skip {
        right: 30px;
        bottom: 20px;
    }

    .page-num {
        position: absolute;
        bottom: 0px;
        left: 20px;
        font-size: 1.2em;
        font-weight: bold;
        color: rgba(95, 95, 95, 1);
    }
</style>