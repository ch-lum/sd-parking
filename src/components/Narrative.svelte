<script>
    import { fade } from "svelte-transitions";
    import Radial from "./Radial.svelte";

    export let page = 0;
    export const lastPage = 9;
    export let data;
    
    const fadeDuration = 500;

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


    function makeRadial(days, areas, padres, scale, size) {
        let subset = data.filter(d => days.includes(d.day_of_week) && areas.includes(d.area) && padres.includes(d.padres_today));

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
</script>

<div id="narrative" in:fade={{ duration: 500 }} out:fade={{ duration: 500, css: (t) => `opacity: ${t*0}` }}>
    <div class="text">
        <p class="page-num">{page} / {lastPage - 1}</p>
        <button class="previous {page === 0 ? 'disabled' : ''}" on:click={previousPage} disabled={page === 0}>Previous</button>
        <button class="next {page === lastPage ? 'disabled' : ''}" on:click={nextPage} disabled={page === lastPage}>Next</button>
        <button class="skip {page === lastPage ? 'disabled' : ''}" on:click={skipToEnd} disabled={page === lastPage}>Skip to end</button>
        
        {#if page===0}
            <div in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <p>Here is a basic radial covering [DAY AND LOCATION]. The text in the center explains what day, and the outer radial shows the time
                It's important to know that the parking volume here is based off the percentage of the highest parking volume recorded on that day of the week, 
                rather than being based off of the raw volume. 
                </p>
            </div>
        {:else if page === 1}
            <div in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <p>Different locations get different colors, comparing [LOCATION 1 AND LOCATION 2] ON [DAY]. Here, you can see the comparison between the usage volume
                between these two locations with different numbers of parking meters. 
                
                </p>
            </div>
        {:else if page === 2}
            <div in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <p>We can also un-normalize, and see the data as an average count for the day rather than looking at a percentage. This is a Monday for each of the locations
                , and you can now see, the heights have changed as the raw number of parking meters matters. 
                </p>
            </div>
        {:else if page === 3}
            <div in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <p>Let's take a look at the East Village. Petco park is Here, home of the Padres. It was actually the construction of the park that revitalized 
                what once was a warehouse district into a vibrant neighborhood full of hotels, events, good food, and of course, amazing views.  But if you want to visit
                here's the average weekday in the East Village and the average weekend. Contrary to what you might expect, the Weekend has fewer people parking</p>
            </div>
        {:else if page === 4}
            <div in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <p>So let's break down our data a little further, and compare every single day. Some things we'd expect, like Fridays being busier than the weekdays that come
                before it. But why doesn't Sundays just don't get any parking?
                 If you've ever been to a parking meter, the sign at the payment station might clue you in. (Parking is free on Sundays!!).</p>
            </div>
        {:else if page === 5}
            <div in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <p>In fact, here's all the locations and their average Sunday, so you can see the Free Parking extends beyond just East Village. </p>
            </div>
        {:else if page === 6}
            <div in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <p>Just for fun, here's the normalized versions of each, so you can see the breakdown as a percentage rather than the raw volume. </p>
            </div>
        {:else if page === 7}
            <div in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <p>But despite Petco Park's vital role in revitalizing East Village, the Padres don't actually influence the avaliability 
                of Street Parking. Choosing a day without a Padres game may seem like a good plan, but the data doesn't support the information. 
                Here's the overall and the East Village, on days where the Padres do and don't play, with the overlayed-versions for comparison.
                It seems like East Village has managed to outgrow its roots, people are interested in everything it has to offer rather than just Baseball. 
                </p>
            </div>
        {:else if page === 8}
            <div in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <p>Now, you're welcome to play with this tool on your own!</p>
            </div>
        {/if}
    </div>
    <div class="radial-box">
        {#if page === 0}
            <Radial {subset} {params} {uniqueId} />
        {/if}
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
</style>