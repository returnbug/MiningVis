<template>
    <div>
        <div>
            <a style="margin-left: 110px; font-size: 14px; font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif; font-weight: 600">Statistics:</a>
            <el-select v-model="value" placeholder="Select" style="width: 250px; margin-left: 10px; margin-top: -3px;">
                <el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value" />
            </el-select>
            <a style="margin-left: 20px; font-size: 14px; font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif; font-weight: 600" >Select Date:</a>
            <el-date-picker v-model="value1" type="monthrange" range-separator="To" start-placeholder="Start month"
                end-placeholder="End month" style="margin-left: 10px; margin-top: -3px;" />
            <el-button style="margin-left: 20px; margin-top: -3px;" color="#A5673F" @click="btn_reset">Reset</el-button>
        </div>
        <div id="time" style="height: 100px; margin-top: -10px; margin-left:-6%;width: 115%;"></div>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import * as echarts from 'echarts'

let myChart
let startValue = null
let endValue = null
let selectedAreaColor = 'rgba(255, 235, 59, 0.3)'
const initChart = () => {
    const chartDom = document.getElementById('time')
    myChart = echarts.init(chartDom);

    const staticData = [
        { name: '2011/01/01', value: ['2011/01/01', 150] },
        { name: '2012/12/31', value: ['2012/12/31', 180] },
        { name: '2013/01/01', value: ['2013/01/01', 190] },
        { name: '2013/12/31', value: ['2013/12/31', 170] },
        { name: '2014/01/01', value: ['2014/01/01', 160] },
        { name: '2014/12/31', value: ['2014/12/31', 150] },
        { name: '2015/01/01', value: ['2015/01/01', 140] },
        { name: '2015/12/31', value: ['2015/12/31', 130] },
        { name: '2016/01/01', value: ['2016/01/01', 120] },
        { name: '2016/12/31', value: ['2016/12/31', 110] },
        { name: '2017/01/01', value: ['2017/01/01', 100] },
        { name: '2017/12/31', value: ['2017/12/31', 90] },
        { name: '2018/01/01', value: ['2018/01/01', 80] },
        { name: '2018/12/31', value: ['2018/12/31', 70] },
        { name: '2019/01/01', value: ['2019/01/01', 60] },
        { name: '2019/12/31', value: ['2019/12/31', 50] },
        { name: '2020/01/01', value: ['2020/01/01', 40] },
        { name: '2020/12/31', value: ['2020/12/31', 30] },
        { name: '2021/01/01', value: ['2021/01/01', 20] },
        { name: '2021/12/31', value: ['2021/12/31', 10] },
        { name: '2022/01/01', value: ['2022/01/01', 20] },
        { name: '2022/12/31', value: ['2022/12/31', 30] },
        { name: '2023/01/01', value: ['2023/01/01', 40] },
        { name: '2023/12/31', value: ['2023/12/31', 50] },
        { name: '2024/01/01', value: ['2024/01/01', 60] },
        { name: '2024/12/31', value: ['2024/12/31', 70] }
    ];

    const yAxisMax = 200
    const yAxisMin = 0
    const interval = 50

    const splitLines = []
    for (let i = yAxisMin; i <= yAxisMax; i += interval) {
        splitLines.push({ interval: i })
    }

    const option = {
        tooltip: {
            trigger: 'axis',
            formatter: function (params) {
                const date = new Date(params[0].name);
                return `${date.getFullYear()}/${date.getMonth() + 1}/${date.getDate()} : ${params[0].value[1]}m`
            },
            axisPointer: {
                animation: false
            }
        },
        xAxis: {
            type: 'time',
            splitLine: {
                show: false
            }
        },
        yAxis: {
            type: 'value',
            boundaryGap: [0, '100%'],
            splitLine: {
                show: true,
                intervals: splitLines
            },
            axisLabel: {
                formatter: function (value) {
                    if (value === 50 || value === 150) {
                        return ''
                    }
                    return `${value}m`
                }
            },
            axisTick: {
                show: true,
                inside: true,
                length: 5
            },
            axisLine: {
                show: true,
                lineStyle: {
                    color: '#333'
                }
            },
            min: yAxisMin,
            max: yAxisMax,
            interval: interval
        },
        series: [
            {
                name: 'Time selection',
                type: 'line',
                showSymbol: false,
                data: staticData,
            }
        ]
    };
    myChart.setOption(option)
    myChart.getZr().on('mousedown', function (params) {
        const pointInGrid = myChart.convertFromPixel({ seriesIndex: 0 }, [params.offsetX, params.offsetY])
        if (pointInGrid) {
            startValue = pointInGrid[0]
        }
        myChart.getZr().on('mousemove', mousemoveHandler)
        myChart.getZr().on('mouseup', mouseupHandler)
    });

    function mousemoveHandler(params) {
        const pointInGrid = myChart.convertFromPixel({ seriesIndex: 0 }, [params.offsetX, params.offsetY])
        if (pointInGrid) {
            endValue = pointInGrid[0]
            updateSelectedArea()
        }
    }

    function mouseupHandler(params) {
        const pointInGrid = myChart.convertFromPixel({ seriesIndex: 0 }, [params.offsetX, params.offsetY])
        if (pointInGrid) {
            endValue = pointInGrid[0]
            updateSelectedArea()
        }
        myChart.getZr().off('mousemove', mousemoveHandler)
        myChart.getZr().off('mouseup', mouseupHandler)
    }

    function updateSelectedArea() {
        if (startValue === null || endValue === null) return

        const minVal = Math.min(startValue, endValue)
        const maxVal = Math.max(startValue, endValue)
        const minDate = new Date(minVal)
        const maxDate = new Date(maxVal)
        value1.value = [minDate, maxDate]

        myChart.setOption({
            series: [{
                markArea: {
                    silent: true,
                    itemStyle: {
                        color: selectedAreaColor
                    },
                    data: [[{
                        xAxis: minVal
                    }, {
                        xAxis: maxVal
                    }]]
                }
            }]
        });
    }
};

const btn_reset = () => {
    value1.value = []
};

onMounted(() => {
    initChart()
});

const value1 = ref([])
const value = ref(6)
const options = [
    { label: 'Energy price index', value: 1 },
    { label: 'Total electricity consumption (GW)', value: 2 },
    { label: 'Mining profit per hash rate (USD)', value: 3 },
    { label: 'Total Blocks', value: 4 },
    { label: 'Number of Mining Pools', value: 5 },
    { label: 'Mining concentration index', value: 6 },
    { label: 'Total Reward (BTC)', value: 7 },
    { label: 'Total Block Reward (BTC)', value: 8 },
    { label: 'Total Transaction Fee (BTC)', value: 9 },
    { label: 'Total Reward (USD)', value: 10 },
    { label: 'Total Block Reward (USD)', value: 11 },
    { label: 'Total Transaction Fee (USD)', value: 12 },
    { label: 'Market Price (USD)', value: 13 },
    { label: 'Market Capitalization (USD)', value: 14 },
    { label: 'Trade Volume (USD)', value: 15 },
    { label: 'Hash Rate (TH/s)', value: 16 },
    { label: 'Difficulty', value: 17 },
    { label: 'Avg Block Size (MB)', value: 18 },
    { label: 'Avg Transactions per Block', value: 19 },
    { label: 'Median Confirmation Time (mins)', value: 20 }
]


</script>

<style></style>