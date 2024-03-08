<script>
    import { onMount } from "svelte";
    import Radial from "./Radial.svelte";
    import * as d3 from "d3";
    import { draggable } from '@neodrag/svelte';
    // export const selectedDay = writable([]);
    // export const selectedPadres = writable([]);
    // export const selectedArea = writable([]);
    let selectedDay = [0, 1, 2, 3, 4, 5, 6];
    let selectedArea = ["East Village", "Hillcrest", "Marina", "Little Italy", "Bankers Hill", "Gaslamp", "Cortez Hill", "Core", "Columbia", "Five Points", "Mission Hills", "University Heights", "North Park", "Cortez", "Talmadge", "College", "Barrio Logan", "Golden Hill", "Point Loma", "Midtown"];
    let selectedPadres = ["True", "False"];

    // $: makeable = $selectedDay.length > 0 && $selectedArea.length > 0 && $selectedPadres.length > 0;
    $: makeable = selectedDay.length > 0 && selectedArea.length > 0 && selectedPadres.length > 0;
    $: radials = [];
    let rad_key = 0;
    let data = [];
    $: console.log(radials)

    onMount(async () => {
        const res = await fetch('rad_by_min.csv');
        const csv = await res.text();
        data = d3.csvParse(csv, d3.autoType);
    });

    function makeRadial() {
        let subset = data.filter(d => selectedDay.includes(d.day_of_week) && selectedArea.includes(d.area) && selectedPadres.includes(d.padres_today));

        const newRadial = {
            subset: subset,
            key: rad_key
        }

        radials = [...radials, newRadial];
        rad_key++
        // console.log(radials);
    }

    
</script>

<div id="machine">
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
            selectedDay = [];
        }}>Reset Day</button>
        <button class="chooser" on:click={() => {
            selectedDay = [0, 1, 2, 3, 4, 5, 6];
        }}>Select All Days</button>
    </div>

    <div class="area">
        <h2>SD Neighborhood</h2>
        <div class="area-text">
            <label>
                <input type="checkbox" bind:group={selectedArea} value="East Village"> East Village<br>
                <input type="checkbox" bind:group={selectedArea} value="Hillcrest"> Hillcrest<br>
                <input type="checkbox" bind:group={selectedArea} value="Marina"> Marina<br>
                <input type="checkbox" bind:group={selectedArea} value="Little Italy"> Little Italy<br>
                <input type="checkbox" bind:group={selectedArea} value="Bankers Hill"> Bankers Hill<br>
                <input type="checkbox" bind:group={selectedArea} value="Gaslamp"> Gaslamp<br>
                <input type="checkbox" bind:group={selectedArea} value="Cortez Hill"> Cortez Hill<br>
                <input type="checkbox" bind:group={selectedArea} value="Core"> Core<br>
                <input type="checkbox" bind:group={selectedArea} value="Columbia"> Columbia<br>
                <input type="checkbox" bind:group={selectedArea} value="Five Points"> Five Points<br>
                <input type="checkbox" bind:group={selectedArea} value="Mission Hills"> Mission Hills<br>
                <input type="checkbox" bind:group={selectedArea} value="University Heights"> University Heights<br>
                <input type="checkbox" bind:group={selectedArea} value="North Park"> North Park<br>
                <input type="checkbox" bind:group={selectedArea} value="Cortez"> Cortez<br>
                <input type="checkbox" bind:group={selectedArea} value="Talmadge"> Talmadge<br>
                <input type="checkbox" bind:group={selectedArea} value="College"> College<br>
                <input type="checkbox" bind:group={selectedArea} value="Barrio Logan"> Barrio Logan<br>
                <input type="checkbox" bind:group={selectedArea} value="Golden Hill"> Golden Hill<br>
                <input type="checkbox" bind:group={selectedArea} value="Point Loma"> Point Loma<br>
                <input type="checkbox" bind:group={selectedArea} value="Midtown"> Midtown <br>
            </label>
        </div>
        <br>
        <button class="chooser" on:click={() => {
            selectedArea = []
        }}>Reset Area</button>

        <button class="chooser" on:click={() => {
            selectedArea = ["East Village", "Hillcrest", "Marina", "Little Italy", "Bankers Hill", "Gaslamp", "Cortez Hill", "Core", "Columbia", "Five Points", "Mission Hills", "University Heights", "North Park", "Cortez", "Talmadge", "College", "Barrio Logan", "Golden Hill", "Point Loma", "Midtown"];
            console.log(selectedArea)
        }}>Select All Areas</button>
    </div>

    <div class="padres">
        <h2>Padres play today?</h2>
        <label>
            <input type="checkbox" bind:group={selectedPadres} value={"True"}> Yes<br>
            <input type="checkbox" bind:group={selectedPadres} value={"False"}> No<br>
        </label>
        <br>
        <button class="chooser" on:click={() => {
            selectedPadres = []
        }}>Reset Padres</button>

        <button class="chooser" on:click={() => {
            selectedPadres = ["True", "False"];
        }}>Select All Games</button>
    </div>

    <button class="maker {!makeable ? 'disabled': ''}" on:click={makeRadial} disabled={!makeable}>Make Radial</button>

    {#each radials as radial (radial.key)}
        <div class="draggable" use:draggable aria-grabbed="true" style="border: 2px solid red">
            <Radial subset={radial.subset}/>
        </div>
    {/each}
</div>

<style>
    #machine {
        padding: 20px;
        font-family: Helvetica;
        font-size: 0.9em;
        display: flex;
        flex-wrap: wrap;
    }

    .day_of_week, .area, .padres {
        border: 2px solid black;
        width: 20%;
        height: 290px;
        overflow: wrap;
        margin-bottom: 20px;
    }

    .area {
        width: 50%;
    }

    .area-text {
        column-count: 3;
    }

    .draggable {
        position: absolute;
        cursor: move;
        user-select: none;
    }
</style>