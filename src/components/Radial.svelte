<script>
    console.log("RADIAL")
    import { onMount, afterUpdate } from "svelte";
    import { rollup } from "d3-array";
    import { draggable } from '@neodrag/svelte'
    // import { selectedDay, selectedArea, selectedPadres } from "./Machine.svelte";
    import * as d3 from "d3";

    export let subset = [];
    export let params = {};
    
    let svg;
    let data;
    const width = 280;
    const height = width;
    const margin = 30;
    const innerRadius = width/8;
    const outerRadius = width/2 - margin;

    onMount(() => {
        const sumByTime = rollup(subset, v => d3.sum(v, leaf => leaf.counts), d => d.time);
        subset = Array.from(sumByTime, ([time, counts]) => ({time, counts}))

        const parseTime = d3.timeParse("%H:%M:%S");
        subset.forEach(d => {
            const parsedTime = parseTime(d.time);
            const today = new Date();
            today.setHours(parsedTime.getHours(), parsedTime.getMinutes(), parsedTime.getSeconds());
            d.time = today;
        });

        const xScale = d3.scaleTime()
            .domain([new Date().setHours(0, 0, 0, 0), new Date().setHours(23, 59, 59, 999)])
            .range([-1 * Math.PI, Math.PI]);
        
        const yScale = d3.scaleRadial()
            .domain([0, d3.max(subset, d => d.counts)])
            .range([innerRadius, outerRadius]);
        
        const scaleScale = {
            "normal": "white",
            "linear": "lightblue",
            "log": "gold"
        }

        const line = d3.lineRadial()
            .curve(d3.curveLinearClosed)
            .angle(d => xScale(d.time))
            .radius(d => yScale(d.counts));
        
        const svg = d3.select("#radial")
            .append("svg")
            .attr("width", width)
            .attr("height", height)
            .attr("viewBox", [-width / 2, -height / 2, width, height])
            .attr("style", `width: {width}; height: auto; font: 10px sans-serif;`)
            .attr("stroke-linejoin", "round")
            .attr("stroke-linecap", "round")
            .attr("background-color", "gray");
        

        svg.append("circle")
            .attr("cx", 0)
            .attr("cy", 0)
            .attr("r", outerRadius + 1)
            .attr("z-index", -1)
            .attr("fill-opacity", 0)
            .attr("stroke", "lightgray");

        svg.append("circle")
            .attr("cx", 0)
            .attr("cy", 0)
            .attr("r", (outerRadius + innerRadius) / 2)
            .attr("fill-opacity", 0)
            .attr("stroke", "lightgray")

        for (let label = 0; label <= 1; label += 0.5) {
            const adjust = (label === 0) ? 10 : -6;

            svg.append("text")
                .attr("x", Math.sin(0))
                .attr("y", Math.cos(0) * (innerRadius + (outerRadius - innerRadius) * label + adjust))
                .style("text-anchor", "middle")
                .style("dominant-baseline", "middle")
                .text(label)
                .style("font-color", "lightgray")
                .attr("background-color", "white");
        }

        for (let hour = 0; hour <= 21; hour += 3) {
            const angle = xScale(new Date().setHours(hour, 0, 0, 0));

            // Add line marker
            svg.append("line")
                .attr("x1", 0)
                .attr("y1", 0)
                .attr("x2", Math.sin(angle) * outerRadius)
                .attr("y2", -1 * Math.cos(angle) * outerRadius)
                .style("stroke", "lightgray")
                .style("stroke-width", "0.75px");

            // Add text marker
            svg.append("text")
                .attr("x", Math.sin(angle) * (outerRadius + 15))
                .attr("y", -1 * Math.cos(angle) * (outerRadius + 15))
                .style("text-anchor", "middle")
                .style("dominant-baseline", "middle")
                .text(hour + ":00")
                .style("font-color", "lightgray");
        }

        svg.append("path")
            .datum(subset)
            .attr("fill", "none")
            .attr("stroke", "steelblue")
            .attr("stroke-width", 1.5)
            .attr("z-index", 1)
            .attr("fill", "lightblue")
            .attr("fill-opacity", 0.2)
            .attr("d", line(subset));

        // Inner circle
        svg.append("circle")
            .attr("cx", 0)
            .attr("cy", 0)
            .attr("r", innerRadius - 1)
            .attr("stroke", "lightgray")
            .attr("fill", scaleScale[params.scale]);
    
        svg.append("text")
            .attr("x", 0)
            .attr("y", 0)
            .attr("text-anchor", "middle")
            .attr("dominant-baseline", "middle")
            .attr("font-size", "12px")
            .text("00:00");

    });
</script>

<div id="radial"></div>

<style>
    #radial {
        /* position: absolute; */
    }
</style>