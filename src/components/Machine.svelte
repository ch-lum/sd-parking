<script>
    import { onMount } from "svelte";
    import Radial from "./Radial.svelte";
    import { draggable } from '@neodrag/svelte';
    import * as d3 from "d3";
    // export const selectedDay = writable([]);
    // export const selectedPadres = writable([]);
    // export const selectedArea = writable([]);
    let selectedDay = [0, 1, 2, 3, 4, 5, 6];
    let selectedArea = ["East Village", "Hillcrest", "Marina", "Little Italy", "Bankers Hill", "Gaslamp", "Cortez Hill", "Core", "Columbia", "Five Points", "Mission Hills", "University Heights", "North Park", "Cortez", "Talmadge", "College", "Barrio Logan", "Golden Hill", "Point Loma", "Midtown"];
    let selectedPadres = ["True", "False"];
    let scale = "normal";
    let radX = 0;
    let radY = 0;

    // $: makeable = $selectedDay.length > 0 && $selectedArea.length > 0 && $selectedPadres.length > 0;
    $: makeable = selectedDay.length > 0 && selectedArea.length > 0 && selectedPadres.length > 0;
    $: radials = [];
    let rad_key = 0;
    export let data = [];
    // $: console.log(radials)

    

    function makeRadial() {
        let subset = data.filter(d => selectedDay.includes(d.day_of_week) && selectedArea.includes(d.area) && selectedPadres.includes(d.padres_today));

        const newRadial = {
            subset: subset,
            position: { x: 0, y: 0 },
            params: {
                selectedDay: selectedDay,
                selectedArea: selectedArea,
                selectedPadres: selectedPadres,
                scale: scale,
                size: "normal",
                type: "machine"
            },
            key: rad_key
        }

        radials = [...radials, newRadial];
        rad_key++
        // console.log(radials);
    }

    function onMouseDown(event) {
        const radial = event.target.closest(".radial");
        if (radial) {
            radial.style.zIndex = 1;
        }
    }

    function onMouseUp(event) {
        console.log('UP')
        const radial = event.target.closest(".radial");
        const snapper = document.querySelector(".snapper");
        const trash = document.querySelector(".trash");
        const mouseLocation = { x: event.clientX, y: event.clientY };
        const snapperRect = snapper.getBoundingClientRect();
        const trashRect = trash.getBoundingClientRect();

        const innerRad = event.target.closest(".inner-rad");
        const rad_id = radials.find(r => r.key === parseInt(innerRad.id.split('-')[1]));
        console.log("rad_id");
        console.log(rad_id.key);

        const overSnapper = mouseLocation.x > snapperRect.width * 50/35 && mouseLocation.x < snapperRect.width * 50/35 + snapperRect.width + 10 && mouseLocation.y > snapperRect.top && mouseLocation.y < snapperRect.bottom;

        const overTrash = mouseLocation.x > snapperRect.width * 50/35 + snapperRect.width + 50 && mouseLocation.x < snapperRect.width * 50/35 + snapperRect.width + trashRect.width + 60 && mouseLocation.y > trashRect.top && mouseLocation.y < trashRect.bottom;      
        
        if (radial && overSnapper) {
            const radialRect = radial.getBoundingClientRect();
            radX = snapperRect.width * 50/35 + snapperRect.width/2 - radialRect.width/2;
            radY = -10;

            rad_id.position.x = radX;
            rad_id.position.y = radY;
            console.log(rad_id.position.x)
            radial.style.transform = `translate(${radX}px, ${radY}px)`;
            radial.style.zIndex = 0;
            innerRad.style.transform = `translate(${0}px, ${0}px)`;
        }

        if (radial && overTrash) {
            console.log("TRASH");
            const index = radials.indexOf(rad_id);
            radials = [...radials.slice(0, index), ...radials.slice(index + 1)];
        }

        
        // console.log(event)
        // const index = radials.indexOf(radial);
        // radials = [...radials.slice(0, index), ...radials.slice(index + 1)];
    }
</script>

<div id="machine">
    <div class="select">
        <div class="day_of_week">
            <h2>Day of week</h2>
            <label>
                <input type="checkbox" bind:group={selectedDay} value={0}> Monday<br>
                <input type="checkbox" bind:group={selectedDay} value={1}> Tuesday<br>
                <input type="checkbox" bind:group={selectedDay} value={2}> Wednesday<br>
                <input type="checkbox" bind:group={selectedDay} value={3}> Thursday<br>
                <input type="checkbox" bind:group={selectedDay} value={4}> Friday<br>
                <input type="checkbox" bind:group={selectedDay} value={5}> Saturday<br>
                <input type="checkbox" bind:group={selectedDay} value={6}> Sunday<br>
            </label>
            <br>

            <button class="chooser" on:click={() => {
                selectedDay = [0, 1, 2, 3, 4, 5, 6];
            }}>Select All</button>
            <button class="chooser" on:click={() => {
                selectedDay = [];
            }}>Clear</button>
        </div>

        <div class="area">
            <h2>SD Neighborhood</h2>
            <div class="area-text">
                <label>
                    <input type="checkbox" bind:group={selectedArea} value="Bankers Hill"> Bankers Hill<br>
                    <input type="checkbox" bind:group={selectedArea} value="Barrio Logan"> Barrio Logan<br>
                    <input type="checkbox" bind:group={selectedArea} value="College"> College<br>
                    <input type="checkbox" bind:group={selectedArea} value="Columbia"> Columbia<br>
                    <input type="checkbox" bind:group={selectedArea} value="Core"> Core<br>
                    <input type="checkbox" bind:group={selectedArea} value="Cortez"> Cortez<br>
                    <input type="checkbox" bind:group={selectedArea} value="Cortez Hill"> Cortez Hill<br>
                    <input type="checkbox" bind:group={selectedArea} value="East Village"> East Village<br>
                    <input type="checkbox" bind:group={selectedArea} value="Five Points"> Five Points<br>
                    <input type="checkbox" bind:group={selectedArea} value="Gaslamp"> Gaslamp<br>
                    <input type="checkbox" bind:group={selectedArea} value="Golden Hill"> Golden Hill<br>
                    <input type="checkbox" bind:group={selectedArea} value="Hillcrest"> Hillcrest<br>
                    <input type="checkbox" bind:group={selectedArea} value="Little Italy"> Little Italy<br>
                    <input type="checkbox" bind:group={selectedArea} value="Marina"> Marina<br>
                    <input type="checkbox" bind:group={selectedArea} value="Midtown"> Midtown <br>
                    <input type="checkbox" bind:group={selectedArea} value="Mission Hills"> Mission Hills<br>
                    <input type="checkbox" bind:group={selectedArea} value="North Park"> North Park<br>
                    <input type="checkbox" bind:group={selectedArea} value="Point Loma"> Point Loma<br>
                    <input type="checkbox" bind:group={selectedArea} value="Talmadge"> Talmadge<br>
                    <input type="checkbox" bind:group={selectedArea} value="University Heights"> University Heights<br>
                </label>
            </div>
            <br>
            <button class="chooser" on:click={() => {
                selectedArea = ["East Village", "Hillcrest", "Marina", "Little Italy", "Bankers Hill", "Gaslamp", "Cortez Hill", "Core", "Columbia", "Five Points", "Mission Hills", "University Heights", "North Park", "Cortez", "Talmadge", "College", "Barrio Logan", "Golden Hill", "Point Loma", "Midtown"];
                // console.log(selectedArea)
            }}>Select All</button>
            <button class="chooser" on:click={() => {
                selectedArea = []
            }}>Clear</button>

        </div>

        <div class="padres">
            <h2>Padres play today?</h2>
            <label>
                <input type="checkbox" bind:group={selectedPadres} value={"True"}> Yes<br>
                <input type="checkbox" bind:group={selectedPadres} value={"False"}> No<br>
            </label>
            <br>
            <button class="chooser" on:click={() => {
                selectedPadres = ["True", "False"];
            }}>Select All</button>
            <button class="chooser" on:click={() => {
                selectedPadres = []
            }}>Clear</button>

        </div>
    </div>

    <div class="interact">
        <div class="makers">
            <select class="maker" bind:value={scale}>
                <option value="normal">Normalized</option>
                <option value="linear_avg">Linear (avg)</option>
                <!-- <option value="linear_sum">Linear (sum)</option> -->
                <!-- <option value="log">Log</option> -->
            </select>

            <button class="maker {!makeable ? 'disabled': ''} green" on:click={makeRadial} disabled={!makeable}>Make Chart</button>
            <button class="maker {radials.length <= 0 ? 'disabled': ''} red" on:click={() => {
                radials = [];
            }} disabled={radials.length <= 0}>Erase All</button>
        </div>

        <div class="charts-container">
            {#each radials as radial (radial.key)}
                <div class="draggable radial" use:draggable={{ position: radial.position, onDrag: ({ offsetX, offsetY }) => radial.position = { x: offsetX, y: offsetY }, }} aria-grabbed="true" on:mouseup={onMouseUp} on:mousedown={onMouseDown} role="presentation">
                    <Radial subset={radial.subset} params={radial.params} uniqueId={`radial-${radial.key}`}/>
                </div>
                <p>{radial.key}</p>
            {/each}
        </div>
        <div class="snapper">
            <h2>Bring disks here</h2>
        </div>
        <div class="trash">
            <h2>Trash</h2>
        </div>
    </div>
</div>

<style>
    #machine {
        padding: 0px;
        font-family: Helvetica;
        font-size: 0.9em;
        height: 940px;
        width: 100%;
    }

    h2 {
        line-height: 25%;
    }

    button:hover {
        color: rgba(58, 58, 58, 0.5);
    }
    .select {
        display: flex;
        flex-wrap: wrap;
        background-color: lightgray;
        padding: 20px
    }

    .day_of_week, .area, .padres {
        width: 20%;
        height: 200px;
        overflow: wrap;
        margin-bottom: 20px;
    }

    .area {
        width: 60%;
    }

    .area-text {
        column-count: 4;
    }

    .draggable {
        position: absolute;
        cursor: move;
        user-select: none;
        margin: 5px;
    }

    .chooser {
        font-size: 0.9em;
        color: rgba(95, 95, 95, 1);
        background-color: rgba(58, 58, 58, 0);
        border: 2px solid rgba(51, 51, 51, 0);
        border-radius: 5px;
        text-decoration: underline dotted;
        font-style: italic;
        z-index: 3;
    }

    .maker {
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
    }

    .green {
        background-color: lightgreen;
    }

    .red {
        background-color: lightcoral;
    }

    .charts-container {
        /* display: flex;
        flex-wrap: wrap;
        justify-content: center;
        align-items: top; */
        height: 360px;
        width: 50%;
    }

    .radial {
        border-radius: 50%;
        top: 340px;
        z-index: 2;
        margin: 0px;
        padding: 0px;
    }

    .snapper {
        width: 35%;
        border: 1px solid darkslategray;
        background-color: #F7F0F5;
        text-align: center;
        padding: 0px;
    }
    
    .trash {
        width: 10%;
        border: 1px solid darkslategray;
        background-color: lightcoral;
        text-align: center;
        margin-left: 40px;
    }

    .interact {
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        align-items: left;
        justify-content: top;
        padding: 20px;
    }
    
    .makers {
        position: absolute;
    }
</style>