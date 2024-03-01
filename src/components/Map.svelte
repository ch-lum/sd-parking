<script>
  import mapbox from 'mapbox-gl';
  import 'mapbox-gl/dist/mapbox-gl.css';
  import { onMount } from 'svelte';
  import * as d3 from 'd3';
  let dataset = []
  
  onMount(() => {
    mapbox.accessToken = "pk.eyJ1IjoiY2gtbHVtIiwiYSI6ImNsc28yeHVhMDBiOTQya3BwejA5N2w5M24ifQ.goNJS9gKumvE34fkNDaW5g";
    const map = new mapbox.Map({
        container: "map",
        style: "mapbox://styles/mapbox/outdoors-v12",
        center: [-117.16, 32.71],
        zoom: 14.5, // starting zoom level
        minZoom: 14,
        maxZoom: 16,
    });

    map.on("load", () => {
		map.addSource("parking_meters", {
			type: "geojson",
			data: "https://raw.githubusercontent.com/ch-lum/sd-parking/5ba586bc80c533d174a90a54f58b8c54ec95960a/static/parkingMeters.geojson",
		});
		map.addLayer({
			id: "parking_meters",
			type: "circle",
			source: "parking_meters",
      paint: {
                    'circle-radius': {
                        'stops': [
                            [14, 1.5],
                            [16, 5]
                        ]

                    },
                  'circle-color': "#0cf0af",
                  'circle-opacity': 0.3,
                  'circle-stroke-color': "#0c67f0",
                  'circle-stroke-width': 0.3

       }
		});
	});

	});

</script>

<main>
  <h1>Parking Meter Map</h1>

  <p>Zoom In For More Details</p>
  <div id="map" style="width: 100%; height: 1280px;"></div>
</main>

<style>
  * {
        text-align: center;
    }
</style>
