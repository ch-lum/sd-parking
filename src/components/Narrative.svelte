<script>
    import { fade } from "svelte-transitions";
    import Radial from "./Radial.svelte";
    import { onMount } from "svelte";

    export let page = 0;
    export const lastPage = 8;
    export let data = [];
    
    const fadeDuration = 500;
    let isMounted = false;
    const neighborhoods = ["Bankers Hill", "Barrio Logan", "College", "Columbia", "Core", "Cortez", "Cortez Hill", "East Village", "Five Points", "Gaslamp", "Golden Hill", "Hillcrest", "Little Italy", "Marina", "Midtown", "Mission Hills", "North Park", "Point Loma", "Talmadge", "University Heights"];

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
        console.log(subset)
        return subset;
    }

    function returnParam(param) {
        console.log('posidfj')
        console.log(param)
        return param;
    }

    let params = [];

    $: {
        switch (page) {
            case 0: {
                params = [];
                params = [
                    {
                        selectedDay: [0, 1, 2, 3, 4, 5, 6],
                        selectedArea: ["Bankers Hill", "Barrio Logan", "College", "Columbia", "Core", "Cortez", "Cortez Hill", "East Village", "Five Points", "Gaslamp", "Golden Hill", "Hillcrest", "Little Italy", "Marina", "Midtown", "Mission Hills", "North Park", "Point Loma", "Talmadge", "University Heights"],
                        selectedPadres: ["True", "False"],
                        scale: "normal",
                        size: "normal",
                        type: "narrative"
                    }
                ]
                break;
            }

            case 1: {
                params = [];
                params = [
                    {
                        selectedDay: [0, 1, 2, 3, 4, 5, 6],
                        selectedArea: ["Bankers Hill"],
                        selectedPadres: ["True", "False"],
                        scale: "normal",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0, 1, 2, 3, 4, 5, 6],
                        selectedArea: ["Barrio Logan"],
                        selectedPadres: ["True", "False"],
                        scale: "normal",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0, 1, 2, 3, 4, 5, 6],
                        selectedArea: ["College"],
                        selectedPadres: ["True", "False"],
                        scale: "normal",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0, 1, 2, 3, 4, 5, 6],
                        selectedArea: ["Columbia"],
                        selectedPadres: ["True", "False"],
                        scale: "normal",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0, 1, 2, 3, 4, 5, 6],
                        selectedArea: ["Core"],
                        selectedPadres: ["True", "False"],
                        scale: "normal",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0, 1, 2, 3, 4, 5, 6],
                        selectedArea: ["Cortez"],
                        selectedPadres: ["True", "False"],
                        scale: "normal",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0, 1, 2, 3, 4, 5, 6],
                        selectedArea: ["Cortez Hill"],
                        selectedPadres: ["True", "False"],
                        scale: "normal",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0, 1, 2, 3, 4, 5, 6],
                        selectedArea: ["East Village"],
                        selectedPadres: ["True", "False"],
                        scale: "normal",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0, 1, 2, 3, 4, 5, 6],
                        selectedArea: ["Five Points"],
                        selectedPadres: ["True", "False"],
                        scale: "normal",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0, 1, 2, 3, 4, 5, 6],
                        selectedArea: ["Gaslamp"],
                        selectedPadres: ["True", "False"],
                        scale: "normal",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0, 1, 2, 3, 4, 5, 6],
                        selectedArea: ["Golden Hill"],
                        selectedPadres: ["True", "False"],
                        scale: "normal",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0, 1, 2, 3, 4, 5, 6],
                        selectedArea: ["Hillcrest"],
                        selectedPadres: ["True", "False"],
                        scale: "normal",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0, 1, 2, 3, 4, 5, 6],
                        selectedArea: ["Little Italy"],
                        selectedPadres: ["True", "False"],
                        scale: "normal",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0, 1, 2, 3, 4, 5, 6],
                        selectedArea: ["Marina"],
                        selectedPadres: ["True", "False"],
                        scale: "normal",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0, 1, 2, 3, 4, 5, 6],
                        selectedArea: ["Midtown"],
                        selectedPadres: ["True", "False"],
                        scale: "normal",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0, 1, 2, 3, 4, 5, 6],
                        selectedArea: ["Mission Hills"],
                        selectedPadres: ["True", "False"],
                        scale: "normal",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0, 1, 2, 3, 4, 5, 6],
                        selectedArea: ["North Park"],
                        selectedPadres: ["True", "False"],
                        scale: "normal",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0, 1, 2, 3, 4, 5, 6],
                        selectedArea: ["Point Loma"],
                        selectedPadres: ["True", "False"],
                        scale: "normal",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0, 1, 2, 3, 4, 5, 6],
                        selectedArea: ["Talmadge"],
                        selectedPadres: ["True", "False"],
                        scale: "normal",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0, 1, 2, 3, 4, 5, 6],
                        selectedArea: ["University Heights"],
                        selectedPadres: ["True", "False"],
                        scale: "normal",
                        size: "small",
                        type: "narrative"
                    },
                ]
                break;
            }

            case 2: {
                params = [];
                params = [
                    {
                        selectedDay: [0],
                        selectedArea: ["Bankers Hill"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0],
                        selectedArea: ["Barrio Logan"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0],
                        selectedArea: ["College"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0],
                        selectedArea: ["Columbia"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0],
                        selectedArea: ["Core"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0],
                        selectedArea: ["Cortez"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0],
                        selectedArea: ["Cortez Hill"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0],
                        selectedArea: ["East Village"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0],
                        selectedArea: ["Five Points"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0],
                        selectedArea: ["Gaslamp"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0],
                        selectedArea: ["Golden Hill"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0],
                        selectedArea: ["Hillcrest"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0],
                        selectedArea: ["Little Italy"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0],
                        selectedArea: ["Marina"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0],
                        selectedArea: ["Midtown"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0],
                        selectedArea: ["Mission Hills"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0],
                        selectedArea: ["North Park"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0],
                        selectedArea: ["Point Loma"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0],
                        selectedArea: ["Talmadge"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0],
                        selectedArea: ["University Heights"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                ]
                break;
            }

            case 3: {
                params = [];
                params = [
                    {
                        selectedDay: [0, 1, 2, 3, 4],
                        selectedArea: ["East Village"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "normal",
                        type: "narrative"
                    },
                    {
                        selectedDay: [5, 6],
                        selectedArea: ["East Village"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "normal",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0, 1, 2, 3, 4],
                        selectedArea: ["East Village"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [5, 6],
                        selectedArea: ["East Village"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    }
                ]
                break;
            
            }

            case 4: {
                params = [];
                params = [
                    {
                        selectedDay: [0],
                        selectedArea: ["East Village"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [1],
                        selectedArea: ["East Village"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [2],
                        selectedArea: ["East Village"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [3],
                        selectedArea: ["East Village"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [4],
                        selectedArea: ["East Village"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [5],
                        selectedArea: ["East Village"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [6],
                        selectedArea: ["East Village"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    
                    
                ];
                break;

            }
             
            case 5: {
                params = [];
                params = [
                    {
                        selectedDay: [6],
                        selectedArea: ["Bankers Hill"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [6],
                        selectedArea: ["Barrio Logan"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [6],
                        selectedArea: ["College"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [6],
                        selectedArea: ["Columbia"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [6],
                        selectedArea: ["Core"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [6],
                        selectedArea: ["Cortez"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [6],
                        selectedArea: ["Cortez Hill"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [6],
                        selectedArea: ["East Village"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [6],
                        selectedArea: ["Five Points"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [6],
                        selectedArea: ["Gaslamp"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [6],
                        selectedArea: ["Golden Hill"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [6],
                        selectedArea: ["Hillcrest"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [6],
                        selectedArea: ["Little Italy"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [6],
                        selectedArea: ["Marina"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [6],
                        selectedArea: ["Midtown"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [6],
                        selectedArea: ["Mission Hills"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [6],
                        selectedArea: ["North Park"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [6],
                        selectedArea: ["Point Loma"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [6],
                        selectedArea: ["Talmadge"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [6],
                        selectedArea: ["University Heights"],
                        selectedPadres: ["True", "False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                ]
                break;
            }

            case 6: {
                params = [];
                params = [
                    {
                        selectedDay: [0, 1, 2, 3, 4, 5],
                        selectedArea: ["East Village"],
                        selectedPadres: ["True"],
                        scale: "linear_avg",
                        size: "normal",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0, 1, 2, 3, 4, 5],
                        selectedArea: ["East Village"],
                        selectedPadres: ["False"],
                        scale: "linear_avg",
                        size: "normal",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0, 1, 2, 3, 4, 5],
                        selectedArea: ["East Village"],
                        selectedPadres: ["True"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                    {
                        selectedDay: [0, 1, 2, 3, 4, 5],
                        selectedArea: ["East Village"],
                        selectedPadres: ["False"],
                        scale: "linear_avg",
                        size: "small",
                        type: "narrative"
                    },
                ]
                break;
            
            }
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
                <p>
                    Here's another way to look at the data. Instead of a timeline, times wrap around the circle with midnight at the bottom and noon at the top. The maximum of this plot has been normalized to the day's maximum, so you can see the relative volume of parking at each time of day. Once again, you can see how most of the parking drops off at 6 PM, with the remaining meters ending at 8 PM.
                </p>
            </div>
        {:else if page === 1}
            <div in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <p>
                    We can further split the data by location, where each location gets its own color. Again, the data is still normalized based on its own maximum, so we can compare how each location grows and shrinks throughout the day. 
                    
                    As pointed out before, Hillcrest, Gaslamp, and the Marina all regularly have parking meters expiring past 6 PM. Further, Five Points has a strange distribution, not having a quick increase early in the morning, instead activating a lot of meters before noon.
                </p>
            </div>
        {:else if page === 2}
            <div in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <p>
                    We can also un-normalize, and see the data as an average count on a day rather than looking at a proportion. Note how the center of each disk has changed, that's one way of telling the difference in scale. That, and looking at the scale. This is a Monday for each of the locations and as we can see, the many of the locations have charts that look just like a circle. This is because they have very few parking meters as a whole and just don't appear on this scale. The blown up line graph might be a better fit to visualize volume than this tiny, faceted version.
                </p>
            </div>
        {:else if page === 3}
            <div in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <p>
                    Let's zoom in on the East Village, the largest of our neighborhoods. Petco Park is in the East Village, home of the Padres. It was actually the construction of Petco Park which revitalized an urban warehouse district into the vibrant area it is today. Below, you'll find the average weekday and the average weekend for parking. In the middle, we overlayed the two to compare the average volumes. You might have caught on already, but think about why fewer parking meters are active on the weekends.
                </p>
            </div>
        {:else if page === 4}
            <div in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <p>
                    A bit of a trick was played on you. If we split the data down further, we can see that Sunday simply doesn't have any parking. This explains why the weekend average is about half that of the weekday average, half of the sample doesn't have any data. You might have experienced this yourself, first parking then remembering that it's free! Parking meters are also free on most federal holidays as well, so go out and park on Memorial Day!
                </p>
            </div>
        {:else if page === 5}
            <div in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <p>
                    Just for further proof of concept, here's all the Sundays. Or are they donut holes? Or golf balls? Is there even data encoded in these? I promise there is, but it's just not very interesting. It's just a circle. In order to add some excitement, I randomized the position of the of the circles. It's a bit of a mess, but the data still just as well-expressed as it was before.
                </p>
            </div>
        {:else if page === 6}
            <div in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <p>
                    Back to the East Village. Our last observation is that we tagged days whether or not there was a Padres home game on that same day. One would think that on those days, parking would be more difficult to find. After all, street parking prices stay the same while private lots' have their prices wildly raised. However, that's not what the data has. There's really no difference in the average volume of parking meters between days with and without a Padres game. Average taken of all days of the week but Sunday.
                </p>
            </div>
        {:else if page === 7}
            <div in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <p>
                    Now, you can try playing with the tool yourself. Compare different locations and days to each other to explore similarities and differences among the different slices of data. Which day of the week gets the most parking? Go to the next page to see under the hood and mess around yourself.
                </p>
            </div>
        {/if}
    </div>

    <div class="radial-box">
        {#if page === 0 && data.length > 0}
            <div class="rad-wrapper" style="width: 100%;" in:fade={{ delay: fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h2>All Locations</h2>
                <Radial subset={makeSubset(params[0])} params={params[0]} uniqueId={"radial-A0"}/>
            </div>

        {:else if page === 1 && data.length > 0}
            <div class="rad-wrapper" style="left: 0%" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Bankers Hill</h3>
                <Radial subset={makeSubset(params[0])} params={params[0]} uniqueId={"radial-B0"}/>
            </div>
            <div class="rad-wrapper" style="left: 12.5%" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Barrio Logan</h3>
                <Radial subset={makeSubset(params[1])} params={params[1]} uniqueId={"radial-B1"}/>
            </div>
            <div class="rad-wrapper" style="left: 25%" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>College</h3>
                <Radial subset={makeSubset(params[2])} params={params[2]} uniqueId={"radial-B2"}/>
            </div>
            <div class="rad-wrapper" style="left: 37.5%" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Columbia</h3>
                <Radial subset={makeSubset(params[3])} params={params[3]} uniqueId={"radial-B3"}/>
            </div>
            <div class="rad-wrapper" style="left: 50%" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Core</h3>
                <Radial subset={makeSubset(params[4])} params={params[4]} uniqueId={"radial-B4"}/>
            </div>
            <div class="rad-wrapper" style="left: 62.5%" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Cortez</h3>
                <Radial subset={makeSubset(params[5])} params={params[5]} uniqueId={"radial-B5"}/>
            </div>
            <div class="rad-wrapper" style="left: 75%" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Cortez Hill</h3>
                <Radial subset={makeSubset(params[6])} params={params[6]} uniqueId={"radial-B6"}/>
            </div>


            <div class="rad-wrapper" style="left: 0%; top: 440px" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>East Village</h3>
                <Radial subset={makeSubset(params[7])} params={params[7]} uniqueId={"radial-B7"}/>
            </div>
            <div class="rad-wrapper" style="left: 12.5%; top: 440px" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Five Points</h3>
                <Radial subset={makeSubset(params[8])} params={params[8]} uniqueId={"radial-B8"}/>
            </div>
            <div class="rad-wrapper" style="left: 25%; top: 440px" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Gaslamp</h3>
                <Radial subset={makeSubset(params[9])} params={params[9]} uniqueId={"radial-B9"}/>
            </div>
            <div class="rad-wrapper" style="left: 37.5%; top: 440px" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Golden Hill</h3>
                <Radial subset={makeSubset(params[10])} params={params[10]} uniqueId={"radial-B10"}/>
            </div>
            <div class="rad-wrapper" style="left: 50%; top: 440px" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Hillcrest</h3>
                <Radial subset={makeSubset(params[11])} params={params[11]} uniqueId={"radial-B11"}/>
            </div>
            <div class="rad-wrapper" style="left: 62.5%; top: 440px" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Little Italy</h3>
                <Radial subset={makeSubset(params[12])} params={params[12]} uniqueId={"radial-B12"}/>
            </div>
            <div class="rad-wrapper" style="left: 75%; top: 440px" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Marina</h3>
                <Radial subset={makeSubset(params[13])} params={params[13]} uniqueId={"radial-B13"}/>
            </div>


            <div class="rad-wrapper" style="left: {12.5 - 12.5/2}%; top: 660px" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Midtown</h3>
                <Radial subset={makeSubset(params[14])} params={params[14]} uniqueId={"radial-B14"}/>
            </div>
            <div class="rad-wrapper" style="left: {25 - 12.5/2}%; top: 660px" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Mission Hills</h3>
                <Radial subset={makeSubset(params[15])} params={params[15]} uniqueId={"radial-15"}/>
            </div>
            <div class="rad-wrapper" style="left: {37.5 - 12.5/2}%; top: 660px" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>North Park</h3>
                <Radial subset={makeSubset(params[16])} params={params[16]} uniqueId={"radial-B16"}/>
            </div>
            <div class="rad-wrapper" style="left: {50 - 12.5/2}%; top: 660px" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Point Loma</h3>
                <Radial subset={makeSubset(params[17])} params={params[17]} uniqueId={"radial-B17"}/>
            </div>
            <div class="rad-wrapper" style="left: {62.5 - 12.5/2}%; top: 660px" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Talmadge</h3>
                <Radial subset={makeSubset(params[18])} params={params[18]} uniqueId={"radial-B18"}/>
            </div>
            <div class="rad-wrapper" style="left: {75 - 12.5/2}%; top: 660px" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>University Heights</h3>
                <Radial subset={makeSubset(params[19])} params={params[19]} uniqueId={"radial-B19"}/>
            </div>

        {:else if page === 2 && data.length > 0}
            <div class="rad-wrapper" style="left: 0%" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Bankers Hill</h3>
                <Radial subset={makeSubset(params[0])} params={params[0]} uniqueId={"radial-C0"}/>
            </div>
            <div class="rad-wrapper" style="left: 12.5%" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Barrio Logan</h3>
                <Radial subset={makeSubset(params[1])} params={params[1]} uniqueId={"radial-C1"}/>
            </div>
            <div class="rad-wrapper" style="left: 25%" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>College</h3>
                <Radial subset={makeSubset(params[2])} params={params[2]} uniqueId={"radial-C2"}/>
            </div>
            <div class="rad-wrapper" style="left: 37.5%" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Columbia</h3>
                <Radial subset={makeSubset(params[3])} params={params[3]} uniqueId={"radial-C3"}/>
            </div>
            <div class="rad-wrapper" style="left: 50%" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Core</h3>
                <Radial subset={makeSubset(params[4])} params={params[4]} uniqueId={"radial-C4"}/>
            </div>
            <div class="rad-wrapper" style="left: 62.5%" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Cortez</h3>
                <Radial subset={makeSubset(params[5])} params={params[5]} uniqueId={"radial-C5"}/>
            </div>
            <div class="rad-wrapper" style="left: 75%" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Cortez Hill</h3>
                <Radial subset={makeSubset(params[6])} params={params[6]} uniqueId={"radial-C6"}/>
            </div>


            <div class="rad-wrapper" style="left: 0%; top: 440px" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>East Village</h3>
                <Radial subset={makeSubset(params[7])} params={params[7]} uniqueId={"radial-C7"}/>
            </div>
            <div class="rad-wrapper" style="left: 12.5%; top: 440px" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Five Points</h3>
                <Radial subset={makeSubset(params[8])} params={params[8]} uniqueId={"radial-C8"}/>
            </div>
            <div class="rad-wrapper" style="left: 25%; top: 440px" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Gaslamp</h3>
                <Radial subset={makeSubset(params[9])} params={params[9]} uniqueId={"radial-C9"}/>
            </div>
            <div class="rad-wrapper" style="left: 37.5%; top: 440px" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Golden Hill</h3>
                <Radial subset={makeSubset(params[10])} params={params[10]} uniqueId={"radial-C10"}/>
            </div>
            <div class="rad-wrapper" style="left: 50%; top: 440px" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Hillcrest</h3>
                <Radial subset={makeSubset(params[11])} params={params[11]} uniqueId={"radial-C11"}/>
            </div>
            <div class="rad-wrapper" style="left: 62.5%; top: 440px" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Little Italy</h3>
                <Radial subset={makeSubset(params[12])} params={params[12]} uniqueId={"radial-C12"}/>
            </div>
            <div class="rad-wrapper" style="left: 75%; top: 440px" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Marina</h3>
                <Radial subset={makeSubset(params[13])} params={params[13]} uniqueId={"radial-C13"}/>
            </div>


            <div class="rad-wrapper" style="left: {12.5 - 12.5/2}%; top: 660px" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Midtown</h3>
                <Radial subset={makeSubset(params[14])} params={params[14]} uniqueId={"radial-C14"}/>
            </div>
            <div class="rad-wrapper" style="left: {25 - 12.5/2}%; top: 660px" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Mission Hills</h3>
                <Radial subset={makeSubset(params[15])} params={params[15]} uniqueId={"radial-C15"}/>
            </div>
            <div class="rad-wrapper" style="left: {37.5 - 12.5/2}%; top: 660px" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>North Park</h3>
                <Radial subset={makeSubset(params[16])} params={params[16]} uniqueId={"radial-C16"}/>
            </div>
            <div class="rad-wrapper" style="left: {50 - 12.5/2}%; top: 660px" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Point Loma</h3>
                <Radial subset={makeSubset(params[17])} params={params[17]} uniqueId={"radial-C17"}/>
            </div>
            <div class="rad-wrapper" style="left: {62.5 - 12.5/2}%; top: 660px" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Talmadge</h3>
                <Radial subset={makeSubset(params[18])} params={params[18]} uniqueId={"radial-C18"}/>
            </div>
            <div class="rad-wrapper" style="left: {75 - 12.5/2}%; top: 660px" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>University Heights</h3>
                <Radial subset={makeSubset(params[19])} params={params[19]} uniqueId={"radial-C19"}/>
            </div>
        {:else if page === 3 && data.length > 0}
            <div class="rad-wrapper" style="width: 50%; left: 5%;" in:fade={{ delay: fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h2>Weekdays in East Village</h2>
                <Radial subset={makeSubset(params[0])} params={params[0]} uniqueId={"radial-D0"}/>
            </div>
            <div class="rad-wrapper" style="width: 50%; left: 45%;" in:fade={{ delay: fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h2>Weekends in East Village</h2>
                <Radial subset={makeSubset(params[1])} params={params[1]} uniqueId={"radial-D1"}/>
            </div>
            <div class="rad-wrapper" style="width: 100%; top: 240px;" in:fade={{ delay: fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Overlay</h3>
                <Radial subset={makeSubset(params[2])} params={params[2]} uniqueId={"radial-D2"}/>
            </div>
            <div class="rad-wrapper" style="width: 100%; top: 240px;" in:fade={{ delay: fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3> </h3>
                <Radial subset={makeSubset(params[3])} params={params[3]} uniqueId={"radial-D3"}/>
            </div>
        {:else if page === 4 && data.length > 0}
            <div class="rad-wrapper" style="left: 0%" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Monday</h3>
                <Radial subset={makeSubset(params[0])} params={params[0]} uniqueId={"radial-E0"}/>
            </div>
            <div class="rad-wrapper" style="left: 12.5%" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Tuesday</h3>
                <Radial subset={makeSubset(params[1])} params={params[1]} uniqueId={"radial-E1"}/>
            </div>
            <div class="rad-wrapper" style="left: 25%" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Wednesday</h3>
                <Radial subset={makeSubset(params[2])} params={params[2]} uniqueId={"radial-E2"}/>
            </div>
            <div class="rad-wrapper" style="left: 37.5%" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Thursday</h3>
                <Radial subset={makeSubset(params[3])} params={params[3]} uniqueId={"radial-E3"}/>
            </div>
            <div class="rad-wrapper" style="left: 50%" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Friday</h3>
                <Radial subset={makeSubset(params[4])} params={params[4]} uniqueId={"radial-E4"}/>
            </div>
            <div class="rad-wrapper" style="left: 62.5%" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Saturday</h3>
                <Radial subset={makeSubset(params[5])} params={params[5]} uniqueId={"radial-E5"}/>
            </div>
            <div class="rad-wrapper" style="left: 75%" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Sunday</h3>
                <Radial subset={makeSubset(params[6])} params={params[6]} uniqueId={"radial-E6"}/>
            </div>
        {:else if page === 5 && data.length > 0}
            {#each neighborhoods as nb, i}
                <div class="rad-wrapper" style="left: {Math.random() * 85}%; top: {Math.random() * 300 + 200}px" in:fade={{ delay:fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                    <h3 style="top: 20px;">{nb}</h3>
                    <Radial subset={makeSubset(params[i])} params={params[i]} uniqueId={`radial-F${i}`}/>
                </div>
            {/each}
        {:else if page === 6 && data.length > 0}
            <div class="rad-wrapper" style="width: 50%; left: 5%;" in:fade={{ delay: fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h2>Padres Played</h2>
                <Radial subset={makeSubset(params[0])} params={params[0]} uniqueId={"radial-G0"}/>
            </div>
            <div class="rad-wrapper" style="width: 50%; left: 45%;" in:fade={{ delay: fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h2>Padres Didn't Play</h2>
                <Radial subset={makeSubset(params[1])} params={params[1]} uniqueId={"radial-G1"}/>
            </div>
            <div class="rad-wrapper" style="width: 100%; top: 240px;" in:fade={{ delay: fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3>Overlay</h3>
                <Radial subset={makeSubset(params[2])} params={params[2]} uniqueId={"radial-G2"}/>
            </div>
            <div class="rad-wrapper" style="width: 100%; top: 240px;" in:fade={{ delay: fadeDuration, duration: fadeDuration }} out:fade={{ duration: fadeDuration }}>
                <h3> </h3>
                <Radial subset={makeSubset(params[3])} params={params[3]} uniqueId={"radial-G3"}/>
            </div>
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
        background-color: white;
        padding: 20px;
        height: 18%;
        position: relative;
        padding-left: 60px;
        padding-right: 60px;
        font-size: 1.2em;
        text-align: justify;        
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
        text-align: center;
        position: absolute;
        /* border: 1px solid grey; */
    }

    h3 {
        position: absolute;
        width: 100%;
    }

</style>