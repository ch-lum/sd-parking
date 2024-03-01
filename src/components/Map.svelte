<script>
  import mapbox from 'mapbox-gl';
  import 'mapbox-gl/dist/mapbox-gl.css';
  import { onMount } from 'svelte';
  import * as d3 from 'd3';
  let meter_data = []
  let meter_markers = []
  let map = []
  
  onMount(() => {
    mapbox.accessToken = "pk.eyJ1IjoiY2gtbHVtIiwiYSI6ImNsc28yeHVhMDBiOTQya3BwejA5N2w5M24ifQ.goNJS9gKumvE34fkNDaW5g";
    const map = new mapbox.Map({
        container: "map",
        style: "mapbox://styles/mapbox/outdoors-v12",
        center: [-117.16, 32.71],
        zoom: 14.5, // starting zoom level
        minZoom: 13,
        maxZoom: 16,
    });

    let metersFile = "https://raw.githubusercontent.com/ch-lum/sd-parking/5ba586bc80c533d174a90a54f58b8c54ec95960a/static/parkingMeters.geojson";
		
    fetch(metersFile)
		.then((response) => response.json())
		.then((d) => {meter_data = d.features})
    .then((d) => create_meter_markers(meter_data));
    
   const marker_container = d3
		.select(map.getCanvasContainer() )
		.append("svg")
		.attr("width", "100%")
		.attr("height", "1280")
    .style("position", "relative")
		.style("z-index", 2);

    function create_meter_markers(meter_data) {
		  meter_markers = marker_container
			.selectAll("circle")
			.data(meter_data)
			.enter()
			.append("circle")
			.style("fill", "#0cf0af")
			.attr("stroke", "#0c67f0")
			.attr("stroke-width", 0.1)
			.attr("fill-opacity", 0.3);
			position_meter_markers();
          }


      function position_meter_markers() {
		meter_markers
			.attr("cx", function (d) {
				return project(d.geometry.coordinates, 13).x
			})
			.attr("cy", function (d) {
        return project(d.geometry.coordinates, 13).y
      })
      .attr("r", function (d) {
        return map.getZoom()-12;
      })
    }

    function project(d) {
		let points = map.project(new mapboxgl.LngLat(+d[0], +d[1]));
    return points
	}
  map.on("viewreset", position_meter_markers);
	map.on("move", position_meter_markers);
	map.on("moveend", position_meter_markers);
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
