<script>
    import { writable } from "svelte/store";
    import { onMount } from "svelte";
    import Radial from "./Radial.svelte";
    import * as d3 from "d3";
    // export const selectedDay = writable([]);
    // export const selectedPadres = writable([]);
    // export const selectedArea = writable([]);
    let selectedDay = [0, 1, 2, 3, 4, 5, 6];
    let selectedArea = ["East Village", "Hillcrest", "Marina", "Little Italy", "Bankers Hill", "Gaslamp", "Cortez Hill", "Core", "Columbia", "Five Points", "Mission Hills", "University Heights", "North Park", "Cortez", "Talmadge", "College", "Barrio Logan", "Golden Hill", "Point Loma", "Midtown"];
    let selectedPadres = ["True", "False"];

    // $: makeable = $selectedDay.length > 0 && $selectedArea.length > 0 && $selectedPadres.length > 0;
    $: makeable = selectedDay.length > 0 && selectedArea.length > 0 && selectedPadres.length > 0;
    $: radial_subset = {};
    let rad_key = 0;
    let data = [];
    $: console.log(radial_subset)

    onMount(async () => {
        const res = await fetch('rad_by_min.csv');
        const csv = await res.text();
        data = d3.csvParse(csv, d3.autoType);
    });

    function makeRadial() {
        let subset = data.filter(d => selectedDay.includes(d.day_of_week) && selectedArea.includes(d.area) && selectedPadres.includes(d.padres_today));
        radial_subset[rad_key] = subset;
        rad_key++
        // console.log(radial_subset);
    }
</script>

<div id="machine">
    <label>
        <input type="checkbox" bind:group={selectedDay} value={0}> Monday
        <input type="checkbox" bind:group={selectedDay} value={1}> Tuesday
        <input type="checkbox" bind:group={selectedDay} value={2}> Wednesday
        <input type="checkbox" bind:group={selectedDay} value={3}> Thursday
        <input type="checkbox" bind:group={selectedDay} value={4}> Friday
        <input type="checkbox" bind:group={selectedDay} value={5}> Saturday
        <input type="checkbox" bind:group={selectedDay} value={6}> Sunday
    </label>

    <label>
        <input type="checkbox" bind:group={selectedArea} value="East Village"> East Village
        <input type="checkbox" bind:group={selectedArea} value="Hillcrest"> Hillcrest
        <input type="checkbox" bind:group={selectedArea} value="Marina"> Marina
        <input type="checkbox" bind:group={selectedArea} value="Little Italy"> Little Italy
        <input type="checkbox" bind:group={selectedArea} value="Bankers Hill"> Bankers Hill
        <input type="checkbox" bind:group={selectedArea} value="Gaslamp"> Gaslamp
        <input type="checkbox" bind:group={selectedArea} value="Cortez Hill"> Cortez Hill
        <input type="checkbox" bind:group={selectedArea} value="Core"> Core
        <input type="checkbox" bind:group={selectedArea} value="Columbia"> Columbia
        <input type="checkbox" bind:group={selectedArea} value="Five Points"> Five Points
        <input type="checkbox" bind:group={selectedArea} value="Mission Hills"> Mission Hills
        <input type="checkbox" bind:group={selectedArea} value="University Heights"> University Heights
        <input type="checkbox" bind:group={selectedArea} value="North Park"> North Park
        <input type="checkbox" bind:group={selectedArea} value="Cortez"> Cortez
        <input type="checkbox" bind:group={selectedArea} value="Talmadge"> Talmadge
        <input type="checkbox" bind:group={selectedArea} value="College"> College
        <input type="checkbox" bind:group={selectedArea} value="Barrio Logan"> Barrio Logan
        <input type="checkbox" bind:group={selectedArea} value="Golden Hill"> Golden Hill
        <input type="checkbox" bind:group={selectedArea} value="Point Loma"> Point Loma
        <input type="checkbox" bind:group={selectedArea} value="Midtown"> Midtown
    </label>

    <label>
        <input type="checkbox" bind:group={selectedPadres} value={"True"}> Padres Today
        <input type="checkbox" bind:group={selectedPadres} value={"False"}> No Padres
    </label>

    <button class="chooser" on:click={() => {
        selectedDay = [];
    }}>Reset Day</button>

    <button class="chooser" on:click={() => {
        selectedArea = []
    }}>Reset Area</button>

    <button class="chooser" on:click={() => {
        selectedPadres = []
    }}>Reset Padres</button>

    <button class="chooser" on:click={() => {
        selectedDay = [0, 1, 2, 3, 4, 5, 6];
    }}>Select All Days</button>

    <button class="chooser" on:click={() => {
        selectedArea = ["East Village", "Hillcrest", "Marina", "Little Italy", "Bankers Hill", "Gaslamp", "Cortez Hill", "Core", "Columbia", "Five Points", "Mission Hills", "University Heights", "North Park", "Cortez", "Talmadge", "College", "Barrio Logan", "Golden Hill", "Point Loma", "Midtown"];
        console.log(selectedArea)
    }}>Select All Areas</button>

    <button class="chooser" on:click={() => {
        selectedPadres = ["True", "False"];
    }}>Select All Games</button>


    <button on:click={() => {
        console.log([selectedDay, selectedArea, selectedPadres]);
    }}>log</button>

    <button class="maker {!makeable ? 'disabled': ''}" on:click={makeRadial} disabled={!makeable}>Make Radial</button>

    {#each Object.values(radial_subset) as subset (subset)}
        <Radial {subset}/>
    {/each}
</div>

<style>

</style>