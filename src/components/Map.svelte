<script>
  import mapbox from 'mapbox-gl';
  import 'mapbox-gl/dist/mapbox-gl.css';
  import { onMount } from 'svelte';

  
  onMount(() => {
    mapbox.accessToken = "pk.eyJ1IjoiY2gtbHVtIiwiYSI6ImNsc28yeHVhMDBiOTQya3BwejA5N2w5M24ifQ.goNJS9gKumvE34fkNDaW5g";
    const map = new mapbox.Map({
        container: "map",
        style: "mapbox://styles/mapbox/outdoors-v12",
        center: [-117.1611, 32.7157],
        zoom: 13, // starting zoom level
        minZoom: 12,
        maxZoom: 15,
    });
	});
</script>

<main>
  <h1>Svelte template</h1>

  <p>Write your HTML here</p>
  <div id="map" style="width: 100%; height: 1280px;"></div>
</main>

<style>
  /* Write your CSS here */
</style>
