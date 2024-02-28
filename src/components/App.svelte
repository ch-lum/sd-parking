<script>
  // Write your JS here, or import other files
  mapboxgl.accessToken = "pk.eyJ1IjoiY2gtbHVtIiwiYSI6ImNsc28yeHVhMDBiOTQya3BwejA5N2w5M24ifQ.goNJS9gKumvE34fkNDaW5g";
	const map = new mapboxgl.Map({
		container: "map",
		style: "mapbox://styles/mapbox/outdoors-v12", 
		center: [-71.0942, 42.3601], 
		zoom: 13, // starting zoom level
		minZoom: 12,
		maxZoom: 15,
	});

  function project(d) {
    return map.project(new mapboxgl.LngLat(+d.lon, +d.lat));
  }
</script>

<main>
  <h1>Svelte template</h1>

  <p>Write your HTML here</p>
</main>

<style>
  /* Write your CSS here */
</style>
