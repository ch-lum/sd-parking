<script>
    console.log("RADIAL")
    import { onMount, afterUpdate } from "svelte";
    import { rollup } from "d3-array";
    import { draggable } from '@neodrag/svelte'
    // import { selectedDay, selectedArea, selectedPadres } from "./Machine.svelte";
    import * as d3 from "d3";

    export let subset = [];
    export let params = {};
    export let uniqueId;

    // $: console.log(params)
    
    let svg;
    let data;
    const width = 280;
    const height = width;
    const margin = 30;
    const innerRadius = width/8;
    const outerRadius = width/2 - margin;
    const maxAvg = (params.type === "narrative" && params.scale === "linear_avg") ? 800: 1600;
    const maxSum = 5000;
    const jitter = 50
    let dx = params.type === "machine" ? Math.random() * jitter - jitter / 2 : 0;
    let dy = params.type === "machine" ? Math.random() * jitter - jitter / 2 : 0;

    const colors = ['#e6194b', '#3cb44b', '#ffe119', '#4363d8', '#f58231', '#911eb4', '#46f0f0', '#f032e6', '#bcf60c', '#fabebe', '#008080', '#e6beff', '#9a6324', '#a9a9a9', '#800000', '#aaffc3', '#808000', '#ffd8b1', '#000075', '#808080']
    const colorMap = {
        "Bankers Hill": colors[0],
        "Barrio Logan": colors[1],
        "College": colors[2],
        "Columbia": colors[3],
        "Core": colors[4],
        "Cortez": colors[5],
        "Cortez Hill": colors[6],
        "East Village": colors[7],
        "Fize Points": colors[8],
        "Gaslamp": colors[9],
        "Golden Hill": colors[10],
        "Hillcrest": colors[11],
        "Little Italy": colors[12],
        "Marina": colors[13],
        "Midtown": colors[14],
        "Mission Hills": colors[15],
        "North Park": colors[16],
        "Point Loma": colors[17],
        "Talmadge": colors[18],
        "University Heights": colors[19]
    }

    const dayMap = {
        0: "Mon.",
        1: "Tues.",
        2: "Wed.",
        3: "Thurs.",
        4: "Fri.",
        5: "Sat.",
        6: "Sun."
    }

    onMount(() => {
        console.log("params");
        console.log(params);

        const sumByTime = rollup(subset, v => d3.sum(v, leaf => leaf.counts), d => d.time);
        subset = Array.from(sumByTime, ([time, counts]) => ({time, counts}))

        const parseTime = d3.timeParse("%H:%M:%S");
        subset.forEach(d => {
            const parsedTime = parseTime(d.time);
            const today = new Date();
            today.setHours(parsedTime.getHours(), parsedTime.getMinutes(), parsedTime.getSeconds());
            d.time = today;
        });

        if (params.scale === "linear_avg") {
            subset.forEach(d => d.counts = d.counts / (params.selectedDay.length * params.selectedPadres.length))
        }

        const xScale = d3.scaleTime()
            .domain([new Date().setHours(0, 0, 0, 0), new Date().setHours(23, 59, 59, 999)])
            .range([-1 * Math.PI, Math.PI]);
        
        const yScaleNormal = d3.scaleRadial()
            .domain([0, d3.max(subset, d => d.counts)])
            .range([innerRadius, outerRadius]);

        const yScaleLinearAvg = d3.scaleRadial()
            .domain([0, maxAvg])
            .range([innerRadius, outerRadius]);

        const yScaleLinearSum = d3.scaleRadial()
            .domain([0, maxSum])
            .range([innerRadius, outerRadius]);
        
        // Probably won't work
        const yScaleLog = d3.scaleLinear()
            .domain([Math.log(1), Math.log(200)]) // log scale domain
            .range([innerRadius, outerRadius])
            .clamp(true);

        const logScale = num => yScaleLog(Math.log(num));
        
        const scaleScale = {
            "normal": "white",
            "linear_avg": "lightblue",
            "linear_sum": "lightgreen",
            "log": "gold"
        }

        const line = d3.lineRadial()
            .curve(d3.curveLinearClosed)
            .angle(d => xScale(d.time))
        
        if (params.scale === "normal")
            line.radius(d => yScaleNormal(d.counts));
        else if (params.scale === "linear_avg")
            line.radius(d => yScaleLinearAvg(d.counts));
        else if (params.scale === "linear_sum")
            line.radius(d => yScaleLinearSum(d.counts));
        else if (params.scale === "log")
            line.radius(d => logScale(d.counts));
        
        // IF I CAN EVER GET THEM SEPARATED, CHANGE HEIGHT
        
        const viewScale = params.size === "normal" ? 1.1 : 1.8;
        const svg = d3.select(`#${uniqueId}`)
            .append("svg")
            .attr("width", width)
            .attr("height", height)
            .attr("viewBox", [-width * viewScale / 2, -height * viewScale/ 2, width * viewScale, height * viewScale])
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

        // Set labels
        for (let tick = 0; tick <= 1; tick += 0.5) {
            const adjust = (tick === 0) ? 10 : -6;

            const max_label = (params.scale === "normal") ? 1 : 
                (params.scale === "linear_avg") ? maxAvg : 
                (params.scale === "linear_sum") ? maxSum : 1;

            svg.append("text")
                .attr("x", Math.sin(0))
                .attr("y", Math.cos(0) * (innerRadius + (outerRadius - innerRadius) * tick + adjust))
                .style("text-anchor", "middle")
                .style("dominant-baseline", "middle")
                .text(max_label * tick)
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
            .attr("stroke", "black")
            .attr("stroke-width", 1)
            .attr("z-index", 1)
            // .attr("fill", "lightblue")
            .attr("fill-opacity", 0.6)
            .attr("d", line(subset))
            .attr("fill", params.selectedArea.length === 1 ? colorMap[params.selectedArea[0]] : "lightblue");

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
            .text(params.selectedDay.length === 1 ? dayMap[params.selectedDay[0]] : params.selectedDay.length === 7 ? "All days" : params.selectedDay.length + " Days");

    });
</script>

<div class="inner-rad" id={uniqueId} style="transform: translate({dx}px, {dy}px);"></div>

<style>
    
</style>