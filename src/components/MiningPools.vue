<template>
    <div>
        <div>
            <div style="display: flex; align-items: center;">
                <a class="minpool-a">Payout Scheme:</a>
                <div style="height: 3px; width: 18px; background-color: rgb(141,211,199); margin-left: 10px;"></div>
                <span style="margin-left: 3px;">PPS</span>
                <div style="height: 3px; width: 18px; background-color: rgb(190,186,218); margin-left: 10px;"></div>
                <span style="margin-left: 3px;">FPPS</span>
                <div style="height: 3px; width: 18px; background-color: rgb(251,128,114); margin-left: 10px;"></div>
                <span style="margin-left: 3px;">PPLNS</span>
                <div style="height: 3px; width: 18px; background-color: rgb(128,177,211); margin-left: 10px;"></div>
                <span style="margin-left: 3px;">Prop</span>
                <div style="height: 3px; width: 18px; background-color: rgb(253,180,98); margin-left: 10px;"></div>
                <span style="margin-left: 3px;">DGM</span>
                <div style="height: 3px; width: 18px; background-color: rgb(255,237,111); margin-left: 10px;"></div>
                <span style="margin-left: 3px;">Score</span>
            </div>
            <div style="display: flex; align-items: center; margin-top: 5px;">
                <a class="minpool-a">Transaction fee:</a>
                <div style="height: 10px; width: 10px; background-color: rgb(244,202,228); margin-left: 10px;"></div>
                <span style="margin-left: 3px;">Kept by pool</span>
                <div style="height: 10px; width: 10px; background-color: rgb(230,245,201); margin-left: 10px;"></div>
                <span style="margin-left: 3px;">Shared</span>
                <div style="height: 10px; width: 10px; background-color: rgb(223,223,223); margin-left: 10px;"></div>
                <span style="margin-left: 3px;">Shared/kept</span>
                <span style="margin-left: 10px;">Sort:</span>
                <el-select v-model="value1" placeholder="Select" style="width: 100px; margin-left: 3px;">
                    <el-option v-for="item in options1" :key="item.value" :label="item.label" :value="item.value" />
                </el-select>
            </div>
        </div>
        <div style="margin-top: 8px;">
            <el-scrollbar class="custom-scrollbar" style="height: 250px; overflow-y: auto;" always>
                <div v-for="(item, index) in seriesName" :key="index" style="width: 96%;">
                    <div style="display: flex; align-items: center;">
                        <a class="chart-text" :style="{ backgroundColor: color[index] }">{{ item }}</a>
                        <el-icon style="margin-left: 10px; color: rgb(118,118,118);">
                            <InfoFilled />
                        </el-icon>
                    </div>
                    <div :id="'chart1-' + index" style="height: 200px; width: 500px; margin-top: -20px;">
                    </div>
                    <el-divider style="margin-top: -40px;" />
                </div>
            </el-scrollbar>
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import * as echarts from 'echarts'

const value1 = ref(3)
const options1 = [
    {
        label: "Minimum",
        value: 1
    },
    {
        label: "Maximum",
        value: 2
    },
    {
        label: "Average",
        value: 3
    },
]

const seriesName = ['F2Pool', 'AntPool', 'BTCcom', 'SlushPool', 'DeepBit',
    'BTCGuild', 'ViaBTC', 'Poolin', 'GHashIO', 'BitFury', 'unknown', 'others'];
const color = ['#1F77B4', '#FF7F0E', '#2CA02C', '#D62728', '#9467BD',
    '#8C564B', '#E377C2', '#A6761D', '#BCBD22', '#0DBECF', '#666666', '#999999'];
const color1 = ['#8dd3c7', '#bebada', '#fb8072', '#80b1d3', '#fdb462', '#ffeda0'];
const color2 = ['#f4cae4', '#e6f5c9', '#dfdfdf'];

const generateData = () => {
    const categories = [];
    const dataBar = [];
    const dataLine = [];
    const randomStartYear = Math.floor(Math.random() * (2021 - 2018)) + 2012;
    const randomEndYear = randomStartYear + 4;
    const value1 = 3;
    const value2 = 7;
    let currentValue = value1;

    for (let year = 2011; year <= 2024; year++) {
        for (let month = 1; month <= 12; month++) {
            const yearMonth = `${year}-${String(month).padStart(2, '0')}`;
            if (year >= randomStartYear && year <= randomEndYear) {
                categories.push(yearMonth);
                dataBar.push(Math.round(Math.random() * 20));
                dataLine.push(currentValue);
            } else {
                categories.push(yearMonth);
                dataBar.push(null);
                dataLine.push(null);
            }
        }
        currentValue = (currentValue === value1) ? value2 : value1;
    }
    return { categories, dataBar, dataLine };
};

const initializeChart = (index, data) => {
    const chartDom = document.getElementById('chart1-' + index);
    const myChart = echarts.init(chartDom);
    const dataIndexes = [];
    data.categories.forEach((category, idx) => {
        if (data.dataBar[idx] !== null && data.dataLine[idx] !== null) {
            dataIndexes.push(idx);
        }
    });
    const minIndex = Math.min(...dataIndexes);
    const maxIndex = Math.max(...dataIndexes);
    const option = {
        tooltip: {
            trigger: 'axis'
        },
        xAxis: {
            type: 'category',
            data: data.categories,
        },
        yAxis: [
            {
                type: 'value',
                scale: true,
                name: 'Market share (%)',
                max: 20,
                min: 0,
                axisLabel: {
                    formatter: function (value) {
                        if (value === 0 || value === 20) {
                            return value;
                        } else {
                            return '';
                        }
                    }
                }
            },
            {
                type: 'value',
                scale: true,
                name: 'Pool fee (%)',
                max: 10,
                min: 0,
                axisLabel: {
                    formatter: function (value) {
                        if (value === 0 || value === 10) {
                            return value;
                        } else {
                            return '';
                        }
                    }
                }
            }
        ],
        series: [
            {
                name: 'Bar Data',
                type: 'bar',
                data: data.dataBar,
                itemStyle: {
                    color: color[index]
                },
                markArea: {
                    silent: true,
                    itemStyle: {
                        color: color2[index % color2.length],
                        opacity: 0.3
                    },
                    data: [
                        [{
                            xAxis: data.categories[minIndex],
                        }, {
                            xAxis: data.categories[maxIndex],
                        }]
                    ]
                }
            },
            {
                name: 'Line Data',
                type: 'line',
                data: data.dataLine,
                showSymbol: false,
                lineStyle: {
                    width: 3
                },
                itemStyle: {
                    color: color1[index % color1.length]
                }
            }
        ],
    };

    myChart.setOption(option);
};

onMounted(() => {
    seriesName.forEach((_, index) => {
        const data = generateData();
        initializeChart(index, data);
    });
});
</script>

<style>
.minpool-a {
    font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
    font-size: 13px;
    font-weight: 600;
}

span {
    font-size: 13px;
}

.chart-text {
    font-size: 13px;
    color: white;
    border-radius: 5px;
    padding: 5px 10px;
    font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
}
</style>
