<script>
    import { onMount } from "svelte";
    import * as d3 from "d3";
    import Map from "./Map.svelte";

    let minutes = [];
    let maxAreaByCategory;

    onMount(async () => {
        const height = 2400;
        const width = 1000;
        const margin = 120;

        const res = await fetch('by_minute.csv'); 
        const csv = await res.text();
        minutes = d3.csvParse(csv, d3.autoType)

        maxAreaByCategory = Array.from(d3.group(minutes, d => d.area), ([key, values]) => ({key, values: d3.max(values, d => d.count)}))
        maxAreaByCategory.sort((a, b) => d3.ascending(a.values, b.values));
        // console.log(maxAreaByCategory);

        const maxAreaMap = new window.Map(maxAreaByCategory.map(d => [d.key, d.values]));
        minutes.sort((a, b) => {
            // Primary sort by the "area" column
            const areaDiff = d3.descending(maxAreaMap.get(a.area), maxAreaMap.get(b.area));
            if (areaDiff !== 0) return areaDiff;

            // Secondary sort by the "minute" column
            return d3.ascending(a.minute, b.minute);
        });

        // console.log(minutes);

        const svg = d3.select("#timeline")
            .append("svg")
            .attr("width", width)
            .attr("height", height)
            .style("background-color", "white");
        

        const xScaleDiscrete = d3.scalePoint()
            .domain(maxAreaByCategory.map(d => d.key))
            .range([0 + margin, width * 0.45])
            .padding(1);

        const xScaleLinear = d3.scaleLinear()
            .domain(d3.extent(minutes.map(d => d.count)))
            .range([0 + margin, 0 + width * 0.75 - margin]);

        const yScale = d3.scaleTime()
            .domain(d3.extent(minutes.map(d => d3.timeParse("%Y-%m-%d %H:%M:%S")(d.time))))
            .range([0 + margin, height - margin]);

        const colorScale = d3.scaleOrdinal(d3.schemeCategory10);
        
        const timeRange = d3.extent(minutes.map(d => d3.timeParse("%Y-%m-%d %H:%M:%S")(d.time)));
        const numHours = (timeRange[1] - timeRange[0]) / 1000 / 60 / 60;

        const xAxisTop = d3.axisTop(xScaleDiscrete);
        const xAxisBottom = d3.axisBottom(xScaleDiscrete);
        const yAxis = d3.axisLeft(yScale)
            .ticks(numHours, "%H:%M")
            .tickFormat(d3.timeFormat("%H:%M"));

        svg.append("g")
            .attr("transform", `translate(0, ${margin})`)
            .call(xAxisTop)
            .selectAll("text")
            .style("text-anchor", "end")
            .attr("dx", "-.8em")
            .attr("dy", ".15em")
            .attr("transform", "rotate(65)")
            .style("fill", function(d) { return colorScale(d); })
            .style("font-weight", "bold")
            .style("text-transform", "uppercase");

        svg.append("g")
            .attr("transform", `translate(0, ${height - margin})`)
            .call(xAxisBottom)
            .selectAll("text")
            .style("text-anchor", "end")
            .attr("dx", "-.8em")
            .attr("dy", ".15em")
            .attr("transform", "rotate(-65)")
            .style("fill", function(d) { return colorScale(d); })
            .style("font-weight", "bold")
            .style("text-transform", "uppercase");

        
        svg.append("g")
            .attr("transform", `translate(${margin}, 0)`)
            .call(yAxis);

        const line = d3.line()
            .x(d => xScaleDiscrete(d.area) + xScaleLinear(d.count) - margin)
            .y(d => yScale(d3.timeParse("%Y-%m-%d %H:%M:%S")(d.time)))
            .curve(d3.curveStepAfter);

        const areas = d3.group(minutes, d => d.area);

        areas.forEach((area, key) => {
            svg.append("path")
                .datum(area)
                .attr("fill", "none")
                .attr("stroke", "black")
                .attr("stroke-width", 1)
                .attr("d", line)
                .attr("fill", colorScale(key))
                .attr("fill-opacity", 0.6)
        });

    });
</script>

<div id="timeline"></div>

<style>
    #timeline {
        position: relative;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        z-index: 1;
        border: 2px solid green;
    }
</style>