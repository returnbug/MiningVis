<template>
    <div>
        <div style="margin-top: 5px;">
            <el-select v-model="value1" multiple collapse-tags collapse-tags-tooltip :max-collapse-tags="4"
                placeholder="Select" style="width: 180px">
                <el-option v-for="item in options1" :key="item.value" :label="item.label" :value="item.value" />
            </el-select>
            <el-button style="margin-left: auto; margin-left: 3px;" color="#E0E1E2" @click="btn">Search</el-button>
        </div>
        <div style="margin-top: 8px;">
            <el-scrollbar class="custom-scrollbar" style="height: 270px; overflow-y: auto;" always>
                <div v-for="(item, index) in filteredOptions" :key="index" style="width: 96%;">
                    <a class="chart-text">{{ item.label }}</a>
                    <div :id="'chart-' + index" style="height: 200px; width: 500px;">
                    </div>
                    <el-divider />
                </div>
            </el-scrollbar>
        </div>
    </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
import * as echarts from 'echarts'

const value1 = ref([])
const options1 = [
    {
        label: "Total electricity consumption (GW)",
        value: 1
    },
    {
        label: "Energy price index",
        value: 2
    },
    {
        label: "Mining profit per hash rate (USD)",
        value: 3
    },
    {
        label: "Total Transaction Fee (BTC)",
        value: 4
    },
    {
        label: "Mining concentration index",
        value: 5
    },
    {
        label: "Total Transaction Fee (USD)",
        value: 6
    },
    {
        label: "Total Block Reward (USD)",
        value: 7
    },
]

const filteredOptions = computed(() => {
    if (value1.value.length === 0) {
        return options1; 
    } else {
        return options1.filter(item => value1.value.includes(item.value))
    }
})

const initCharts = () => {
    options1.forEach((item, index) => {
        const chartDom = document.getElementById('chart-' + index)
        if (chartDom) {
            const myChart = echarts.init(chartDom)
            let base = +new Date(2011, 1, 1)
            const endDate = +new Date(2024, 11, 31)
            const oneDay = 24 * 3600 * 1000
            const data = [[base, Math.random() * 300 + 1]];
            while (base <= endDate) {
                const now = new Date(base)
                const lastValue = data[data.length - 1][1];
                data.push([+now, Math.max(Math.round((Math.random() - 0.5) * 20 + lastValue), 1)])
                base += oneDay
            }
            const maxDataValue = Math.max(...data.map(item => item[1]))

            const option = {
                tooltip: {
                    trigger: 'axis',
                    position: (pt) => [pt[0], '10%']
                },
                toolbox: {
                    feature: {
                        dataZoom: { yAxisIndex: 'none' },
                        restore: {},
                        saveAsImage: {}
                    }
                },
                xAxis: { type: 'time', boundaryGap: false },
                yAxis: {
                    type: 'value',
                    min: 0,
                    max: maxDataValue, 
                    boundaryGap: [0, '100%'],
                    axisLabel: {
                        interval: true,
                        formatter: (value) => {
                            if (value === 0 || value === maxDataValue) {
                                return value;
                            } else {
                                return '';
                            }
                        }
                    }
                },
                dataZoom: [
                    { type: 'inside', start: 0, end: 20 },
                    { start: 0, end: 20 }
                ],
                series: [
                    {
                        name: 'Fake Data',
                        type: 'line',
                        smooth: true,
                        symbol: 'none',
                        areaStyle: {},
                        data,
                        lineStyle: {
                            color: '#A0A0A0' 
                        },
                        itemStyle: {
                            color: '#A0A0A0' 
                        }
                    }
                ]
            }
            myChart.setOption(option)
        }
    })
}

const btn = () => {
    initCharts()
}

onMounted(() => {
    initCharts()
})
</script>

<style scoped>
.chart-text {
    font-size: 13px;
    color: white;
    background-color: rgb(118, 118, 118);
    border-radius: 5px;
    padding: 5px 10px;
    font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
}
</style>
