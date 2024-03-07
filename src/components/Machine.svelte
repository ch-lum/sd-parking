<script>
    import { writable } from "svelte/store";
    import Radial from "./Radial.svelte";
    export const selectedDay = writable(null);
    export const selectedPadres = writable(null);
    export const selectedArea = writable(null);
</script>

<div id="machine">
    <label>
        <input type="checkbox" bind:checked={$selectedDay} value="Monday"> Monday
        <input type="checkbox" bind:checked={$selectedDay} value="Tuesday"> Tuesday
        <input type="checkbox" bind:checked={$selectedDay} value="Wednesday"> Wednesday
        <input type="checkbox" bind:checked={$selectedDay} value="Thursday"> Thursday
        <input type="checkbox" bind:checked={$selectedDay} value="Friday"> Friday
        <input type="checkbox" bind:checked={$selectedDay} value="Saturday"> Saturday
        <input type="checkbox" bind:checked={$selectedDay} value="Sunday"> Sunday
    </label>

    <label>
        <input type="checkbox" bind:checked={$selectedArea} value="East Village"> East Village
        <input type="checkbox" bind:checked={$selectedArea} value="Hillcrest"> Hillcrest
        <input type="checkbox" bind:checked={$selectedArea} value="Marina"> Marina
        <input type="checkbox" bind:checked={$selectedArea} value="Little Italy"> Little Italy
        <input type="checkbox" bind:checked={$selectedArea} value="Bankers Hill"> Bankers Hill
        <input type="checkbox" bind:checked={$selectedArea} value="Gaslamp"> Gaslamp
        <input type="checkbox" bind:checked={$selectedArea} value="Cortez Hill"> Cortez Hill
        <input type="checkbox" bind:checked={$selectedArea} value="Core"> Core
        <input type="checkbox" bind:checked={$selectedArea} value="Columbia"> Columbia
        <input type="checkbox" bind:checked={$selectedArea} value="Five Points"> Five Points
        <input type="checkbox" bind:checked={$selectedArea} value="Mission Hills"> Mission Hills
        <input type="checkbox" bind:checked={$selectedArea} value="University Heights"> University Heights
        <input type="checkbox" bind:checked={$selectedArea} value="North Park"> North Park
        <input type="checkbox" bind:checked={$selectedArea} value="Cortez"> Cortez
        <input type="checkbox" bind:checked={$selectedArea} value="Talmadge"> Talmadge
        <input type="checkbox" bind:checked={$selectedArea} value="College"> College
        <input type="checkbox" bind:checked={$selectedArea} value="Barrio Logan"> Barrio Logan
        <input type="checkbox" bind:checked={$selectedArea} value="Golden Hill"> Golden Hill
        <input type="checkbox" bind:checked={$selectedArea} value="Point Loma"> Point Loma
        <input type="checkbox" bind:checked={$selectedArea} value="Midtown"> Midtown
    </label>

    <label>
        <input type="checkbox" bind:checked={$selectedPadres} value="Padres Today"> Padres Today
        <input type="checkbox" bind:checked={$selectedPadres} value="No Padres"> No Padres
    </label>

    <Radial {selectedDay} {selectedArea} {selectedPadres} />
</div>

<style>

</style>