<template>
    <div>
        <div>
            <a style="margin-left: 150px; font-weight: 500;">Measure:</a>
            <el-select v-model="value1" placeholder="Select" style="width: 200px; margin-left: 10px;">
                <el-option v-for="item in options1" :key="item.value" :label="item.label" :value="item.value" />
            </el-select>
            <a style="margin-left: 20px; font-weight: 500;">Group by:</a>
            <el-select v-model="value2" placeholder="Select" style="width: 200px; margin-left: 10px;">
                <el-option v-for="item in options2" :key="item.value" :label="item.label" :value="item.value" />
            </el-select>
            <a style="margin-left: 20px; font-weight: 500;">Color by:</a>
            <el-select v-model="value3" placeholder="Select" style="width: 200px; margin-left: 10px;">
                <el-option v-for="item in options3" :key="item.value" :label="item.label" :value="item.value" />
            </el-select>
        </div>
        <div style="margin-top: 5px;">
            <el-row>
                <el-col :span="4">

                </el-col>
                <el-col :span="20">
                    <div ref="chart"></div>
                </el-col>
            </el-row>
        </div>
    </div>
</template>
<script setup>
import {ref, onMounted} from 'vue'
import * as d3 from 'd3'

const chart = ref(null); 
const data = [
  { date: new Date('2023-01-01'), industry: 'Tech', unemployed: 100 },
  { date: new Date('2023-01-01'), industry: 'Healthcare', unemployed: 50 },
];

onMounted(() => {
  drawChart()
});

const drawChart = () => {
  const width = 850;
  const height = 400;
  const marginTop = 10;
  const marginRight = 10;
  const marginBottom = 20;
  const marginLeft = 60; 
  const series = d3.stack()
    .keys(d3.union(data.map(d => d.industry)))
    .value(([, D], key) => D.get(key).unemployed)(d3.index(data, d => d.date, d => d.industry));

  const x = d3.scaleUtc()
    .domain(d3.extent(data, d => d.date))
    .range([marginLeft, width - marginRight]);

  const y = d3.scaleLinear()
    .domain([0, d3.max(series, d => d3.max(d, d => d[1]))])
    .rangeRound([height - marginBottom, marginTop]);

  const color = d3.scaleOrdinal()
    .domain(series.map(d => d.key))
    .range(d3.schemeTableau10);

  const area = d3.area()
    .x(d => x(d.data[0]))
    .y0(d => y(d[0]))
    .y1(d => y(d[1]));

  const svg = d3.select(chart.value)
    .append("svg")
    .attr("width", width)
    .attr("height", height)
    .attr("viewBox", [0, 0, width, height])
    .attr("style", "max-width: 100%; height: auto;");

  svg.append("g")
    .selectAll()
    .data(series)
    .join("path")
    .attr("fill", d => color(d.key))
    .attr("d", area)
    .append("title")
    .text(d => d.key);

  svg.append("g")
    .attr("transform", `translate(0,${height - marginBottom})`)
    .call(d3.axisBottom(x).tickSizeOuter(0));

  svg.append("g")
    .attr("transform", `translate(${marginLeft},0)`)
    .call(d3.axisLeft(y).ticks(height / 80))
    .call(g => g.select(".domain").remove())
    .call(g => g.selectAll(".tick line").clone()
      .attr("x2", width - marginLeft - marginRight)
      .attr("stroke-opacity", 0.1))
    .call(g => g.append("text")
      .attr("x", -marginLeft)
      .attr("y", 10)
      .attr("fill", "currentColor")
      .attr("text-anchor", "start"));
};

const value1 = ref(1)
const value2 = ref(1)
const value3 = ref(1)
const options1 = [
    {
        label:"Market share(%)",
        value:1
    },
    {
        label:"Hash rate(TH/s)",
        value:2
    },
    {
        label:"Electricity(GW)",
        value:3
    },
    {
        label:"Total reward(BTC)",
        value:4
    },
    {
        label:"Total reward(USD)",
        value:5
    },
    {
        label:"Transaction fees(BTC)",
        value:6
    },
    {
        label:"Transaction fees(USD)",
        value:7
    },
]
const options2 = [
    {
        label:"Mining pool",
        value:1
    },
    {
        label:"Payout scheme",
        value:2
    },
    {
        label:"Location",
        value:3
    },
]
const options3 = [
    {
        label:"Mining pool",
        value:1
    },
    {
        label:"Payout scheme",
        value:2
    },
    {
        label:"Location",
        value:3
    },
]

</script>
<style></style>