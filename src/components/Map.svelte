<script>
  import mapbox from "mapbox-gl";
  import "mapbox-gl/dist/mapbox-gl.css";
  import { onMount } from "svelte";
  import * as d3 from "d3";

  let intervalId;

  onMount(() => {
    mapbox.accessToken = "pk.eyJ1IjoiY2gtbHVtIiwiYSI6ImNsc28yeHVhMDBiOTQya3BwejA5N2w5M24ifQ.goNJS9gKumvE34fkNDaW5g";
    const map = new mapbox.Map({
      container: "map",
      style: "mapbox://styles/mapbox/light-v11",
      center: [-117.16, 32.71],
      zoom: 15.5,
      minZoom: 13,
      maxZoom: 16,
    })

    let metersFile = "https://raw.githubusercontent.com/ch-lum/sd-parking/5ba586bc80c533d174a90a54f58b8c54ec95960a/static/parkingMeters.geojson";
    fetch(metersFile)
      .then((response) => response.json())
      .then((data) => {
        console.log(data);
        map.on("load", () => {
          map.addSource("meters", {
            type: "geojson",
            data: data,
          });
          map.addLayer({
            id: "meters",
            type: "circle",
            source: "meters",
            paint: {
              "circle-color": "#0cf0af",
              "circle-stroke-color": "#0c67f0",
              "circle-stroke-width": 0.1,
              "circle-opacity": 0.3,
            },
          });

          let currentFeatureIndex = 0;
          intervalId = setInterval(() => {
            let feature = data.features[currentFeatureIndex];
            map.flyTo({ center: feature.geometry.coordinates, speed: 0.01 });
            currentFeatureIndex = (currentFeatureIndex + 5) % data.features.length;
          }, 2000); // Change the map's center every 5 seconds.
        });

        map.on("dragstart", () => {
          clearInterval(intervalId); // Stop panning when the map is dragged.
        });
      });

  })
</script>

<div id="map"></div>

<style>
  #map {
    position: absolute;
    top: 0;
    bottom: 0;
    width: 100%;
  }
</style>