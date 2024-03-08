<script>
  import mapbox from "mapbox-gl";
  import "mapbox-gl/dist/mapbox-gl.css";
  import { onMount } from "svelte";
  import * as d3 from "d3";

  let intervalId;
  const colors = ['#e6194b', '#3cb44b', '#ffe119', '#4363d8', '#f58231', '#911eb4', '#46f0f0', '#f032e6', '#bcf60c', '#fabebe', '#008080', '#e6beff', '#9a6324', '#a9a9a9', '#800000', '#aaffc3', '#808000', '#ffd8b1', '#000075', '#808080']

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
          const uniquePoles = new Set();

          data.features = data.features.filter((feature) => {
            if (uniquePoles.has(feature.properties.pole)) {
              return false;
            }
            uniquePoles.add(feature.properties.pole);
            return true;
          });

          map.addSource("meters", {
            type: "geojson",
            data: data,
          });
          map.addLayer({
            id: "meters",
            type: "circle",
            source: "meters",
            paint: {
              "circle-color": [
                "match",
                ["get", "area"],
                "Bankers Hill", colors[0],
                "Barrio Logan", colors[1],
                "College", colors[2],
                "Columbia", colors[3],
                "Core", colors[4],
                "Cortez", colors[5],
                "Cortez Hill", colors[6],
                "East Village", colors[7],
                "Fize Points", colors[8],
                "Gaslamp", colors[9],
                "Golden Hill", colors[10],
                "Hillcrest", colors[11],
                "Little Italy", colors[12],
                "Marina", colors[13],
                "Midtown", colors[14],
                "Mission Hills", colors[15],
                "North Park", colors[16],
                "Point Loma", colors[17],
                "Talmadge", colors[18],
                "University Heights", colors[19],
                "#0c67f0"
              ],
              "circle-stroke-color": "darkslategray",
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
    left: 0;
    width: 100%;
    height: 100%;
  }
</style>
