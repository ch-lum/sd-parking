<script>
    import { fade } from "svelte-transitions";
    import Radial from "./Radial.svelte";
    import { onMount } from "svelte";

    export let page = 0;
    export const lastPage = 9;
    export let data = [];
    
    const fadeDuration = 500;
    let isMounted = false;

    onMount(() => {
        isMounted = true;
    });

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

    function makeSubset(param) {
        console.log('subset')
        console.log(param)
        let subset = data.filter(d => param.selectedDay.includes(d.day_of_week) && param.selectedArea.includes(d.area) && param.selectedPadres.includes(d.padres_today));
        console.log(data)
        return subset;
    }

    function makeRadial(param) {
        let subset = data.filter(d => param.selectedDay.includes(d.day_of_week) && param.selectedArea.includes(d.area) && param.selectedPadres.includes(d.padres_today));

        const newRadial = {
            subset: subset,
            params: {
                selectedDay: days,
                selectedArea: areas,
                selectedPadres: padres,
                scale: scale,
                size: size,
            },
            key: rad_key
        }

        // radials = [...radials, newRadial];
        rad_key++;
        // console.log(radials);
    }

    let params = [];

    $: {
        if (page === 0) {
            params = [];
            params = [
                {
                    selectedDay: [0, 1, 2, 3, 4, 5, 6],
                    selectedArea: ["Bankers Hill", "Barrio Logan", "College", "Columbia", "Core", "Cortez", "Cortez Hill", "East Village", "Fize Points", "Gaslamp", "Golden Hill", "Hillcrest", "Little Italy", "Marina", "Midtown", "Mission Hills", "North Park", "Point Loma", "Talmadge", "University Heights"],
                    selectedPadres: [0, 1],
                    scale: "normal",
                    size: "normal"
                }
            ]
        }
    }
</script>

<div id="narrative" in:fade={{ duration: 500 }} out:fade={{ duration: 500, css: (t) => `opacity: ${t*0}` }}>
    <div class="text">
        <p class="page-num">{page} / {lastPage - 1}</p>
        <button class="previous {page === 0 ? 'disabled' : ''}" on:click={previousPage} disabled={page === 0}>Previous</button>
        <button class="next {page === lastPage ? 'disabled' : ''}" on:click={nextPage} disabled={page === lastPage}>Next</button>
        <button class="skip {page === lastPage ? 'disabled' : ''}" on:click={skipToEnd} disabled={page === lastPage}>Skip to end</button>
        
        {#if page===0}
            <div in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <p>Start with overall radial. Explain what you're looking at--explain normalized (not linear yet)</p>
            </div>
        {:else if page === 1}
            <div in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <p>Different locations get different colors. How they're different from each other. How this is a different version of the prior graph, but normalized. [EXPLAIN THIS]</p>
            </div>
        {:else if page === 2}
            <div in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <p>We can also un-normalize. This is a monday for each of the locations.</p>
            </div>
        {:else if page === 3}
            <div in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <p>Let's take a look at the East Village. [DESCRIBE EAST VILLAGE]. Petco park is here, home of the Padres. We can further look day-by-day at the totals. Here's the average weekday in the East Village and the average weekend. Weekends appear to have fewer people parking on average</p>
            </div>
        {:else if page === 4}
            <div in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <p>If we split by day of week, we'll see that we weren't looking close enough. [EACH DAY OF THE WEEK FOR EAST VILLAGE]. Sundays just don't get any parking. If you have ever tried street parking yourself, you might know why (Hint: parking is free on Sundays).</p>
            </div>
        {:else if page === 5}
            <div in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <p>In fact, here's all the locations and their average sunday. Unsurprisingly, there's nothing really there</p>
            </div>
        {:else if page === 6}
            <div in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <p>Just for fun, here's the normalized versions of each.</p>
            </div>
        {:else if page === 7}
            <div in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <p>Last observation, the Padres playing a home game does not really affect the number of people parking in San Diego. Here's the overall and the East Village, with the overlayed-versions in the center,.</p>
            </div>
        {:else if page === 8}
            <div in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <p>Now, you're welcome to play with this tool on your own!</p>
            </div>
        {/if}
    </div>
    <div class="radial-box">
        <!-- {#if page === 0 && isMounted}
            <div class="rad-wrapper">
                <h2>All Locations</h2>
                <Radial subset={makeSubset(params[0])} params={params[0]}, uniqueId={"a"}/>
            </div>
        {/if} -->
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
        padding-left: 400px;
        padding-right: 400px;
        font-size: 1.4em;
    }

    button {
        font-size: 0.8em;
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

    .rad-wrapper {
        /* border: 2px solid blue; */
    }
</style>