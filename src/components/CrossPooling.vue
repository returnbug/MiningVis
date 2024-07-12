<template>
    <div>
        <el-row>
            <el-col :span="5">
                <div style="margin-top: 7px;">
                    <span
                        style="color: white; background-color: rgb(0,128,128); font-size: 10px; padding-top: 2px; padding-bottom: 2px;">&nbsp;%
                        Enter&nbsp;</span>
                    <span
                        style="color: white; background-color: rgb(102,179,179); font-size: 10px; margin-left: 3px; padding-top: 2px; padding-bottom: 2px;">&nbsp;%
                        Hop in&nbsp;</span>
                </div>
                <div>
                    <span
                        style="color: white; background-color: rgb(0,128,128); font-size: 10px; padding-top: 2px; padding-bottom: 2px;">&nbsp;%
                        Exit&nbsp;</span>
                    <span
                        style="color: white; background-color: rgb(102,179,179); font-size: 10px; margin-left: 3px; padding-top: 2px; padding-bottom: 2px;">&nbsp;%
                        Hop out&nbsp;</span>
                </div>
                <div>
                    <span
                        style="color: white; background-color: rgb(0,128,128); font-size: 10px; padding-top: 2px; padding-bottom: 2px;">&nbsp;%
                        Cross pooling&nbsp;</span>
                </div>
            </el-col>
            <el-col :span="16" style="margin-top: -15px;">
                <div ref="chart"></div>
            </el-col>
        </el-row>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import * as d3 from 'd3';

const chart = ref(null);

onMounted(() => {
    const width = 280;  
    const height = width;
    const data = {
        names: ["Apple", "HTC", "Huawei", "LG", "Nokia", "Samsung", "Sony", "Other"],
        colors: ["#c4c4c4", "#69b40f", "#ec1d25", "#c8125c", "#008fc8", "#10218b", "#134b24", "#737373"],
        matrix: [
            [.096899, .008859, .000554, .004430, .025471, .024363, .005537, .025471],
            [.001107, .018272, .000000, .004983, .011074, .010520, .002215, .004983],
            [.000554, .002769, .002215, .002215, .003876, .008306, .000554, .003322],
            [.000554, .001107, .000554, .012182, .011628, .006645, .004983, .010520],
            [.002215, .004430, .000000, .002769, .104097, .012182, .004983, .028239],
            [.011628, .026024, .000000, .013843, .087486, .168328, .017165, .055925],
            [.000554, .004983, .000000, .003322, .004430, .008859, .017719, .004430],
            [.002215, .007198, .000000, .003322, .016611, .014950, .001107, .054264]
        ]
    };

    const outerRadius = Math.min(width, height) * 0.5 - 60;
    const innerRadius = outerRadius - 5;
    const totalValue = d3.sum(data.matrix.flat());
    const tickStep = totalValue * 0.10;
    const formatValue = d3.format(".1~%");

    const chord = d3.chord()
        .padAngle(10 / innerRadius)
        .sortSubgroups(d3.descending)
        .sortChords(d3.descending);

    const arc = d3.arc()
        .innerRadius(innerRadius)
        .outerRadius(outerRadius);

    const ribbon = d3.ribbon()
        .radius(innerRadius - 1)
        .padAngle(1 / innerRadius);

    const color = d3.scaleOrdinal(data.names, data.colors);

    const svg = d3.select(chart.value)
        .append("svg")
        .attr("width", width)
        .attr("height", height)
        .attr("viewBox", [-width / 2, -height / 2, width, height])
        .attr("style", "width: 100%; height: auto; font: 7px sans-serif;");

    const chords = chord(data.matrix);

    const group = svg.append("g")
        .selectAll("g")
        .data(chords.groups)
        .join("g");

    group.append("path")
        .attr("fill", d => color(data.names[d.index]))
        .attr("d", arc);

    group.append("title")
        .text(d => `${data.names[d.index]}\n${formatValue(d.value)}`);

    const groupTick = group.append("g")
        .selectAll("g")
        .data(d => groupTicks(d, tickStep))
        .join("g")
        .attr("transform", d => `rotate(${d.angle * 180 / Math.PI - 90}) translate(${outerRadius},0)`);

    groupTick.append("line")
        .attr("stroke", "currentColor")
        .attr("x2", 6);

    groupTick.append("text")
        .attr("x", 8)
        .attr("dy", "0.35em")
        .attr("transform", d => d.angle > Math.PI ? "rotate(180) translate(-16)" : null)
        .attr("text-anchor", d => d.angle > Math.PI ? "end" : null)
        .text(d => formatValue(d.value));

    group.select("text")
        .attr("font-weight", "bold")
        .text(function (d) {
            return this.getAttribute("text-anchor") === "end"
                ? `↑ ${data.names[d.index]}`
                : `${data.names[d.index]} ↓`;
        });

    svg.append("g")
        .attr("fill-opacity", 0.8)
        .selectAll("path")
        .data(chords)
        .join("path")
        .style("mix-blend-mode", "multiply")
        .attr("fill", d => color(data.names[d.source.index]))
        .attr("d", ribbon)
        .append("title")
        .text(d => `${formatValue(d.source.value)} ${data.names[d.target.index]} → ${data.names[d.source.index]}${d.source.index === d.target.index ? "" : `\n${formatValue(d.target.value)} ${data.names[d.source.index]} → ${data.names[d.target.index]}`}`);

    function groupTicks(d, step) {
        const k = (d.endAngle - d.startAngle) / d.value;
        return d3.range(0, d.value, step).map(value => {
            return { value: value, angle: value * k + d.startAngle };
        });
    }
});
</script>

<style></style>