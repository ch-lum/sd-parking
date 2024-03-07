<script>
    import { onMount, afterUpdate } from "svelte";
    // import { selectedDay, selectedArea, selectedPadres } from "./Machine.svelte";
    import * as d3 from "d3";

    export let selectedDay;
    export let selectedArea;
    export let selectedPadres;

    let svg;
    let data;
    const width = 200;
    const height = 200;

    let updateChart = () => {
        console.log("updateChart");
        d3.select(svg).selectAll("*").remove();

        let filteredData = data;
        selectedDay.subscribe((value) => {
            if (value) {
                filteredData = filteredData.filter((d) => d.day_of_week === value);
            }
        });
        selectedArea.subscribe((value) => {
            if (value) {
                filteredData = filteredData.filter((d) => d.area === value);
            }
        });
        selectedPadres.subscribe((value) => {
            if (value) {
                filteredData = filteredData.filter((d) => d.padres_today === value);
            }
        });

        let pie = d3.pie()
            .value((d) => d.counts)
            .sort(null);
        let arc = d3.arc()
            .innerRadius(0)
            .outerRadius(Math.min(width, height) / 2 - 1);
        let g = d3.select(svg).append("g")
            .attr("transform", `translate(${width / 2}, ${height / 2})`);
        g.selectAll("path")
            .data(pie(filteredData))
            .enter().append("path")
            .attr("d", arc)
            .style("fill", "black");
        
    };

    onMount(async () => {
        const res = await fetch('rad_by_min.csv');
        const csv = await res.text();
        data = d3.csvParse(csv, d3.autoType);
        
        updateChart();
    });

    afterUpdate(updateChart);

</script>

<svg bind:this={svg} width={width} height={height}></svg>