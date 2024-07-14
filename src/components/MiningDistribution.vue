<template>
    <div>
        <div>
            <a
                style="margin-left: 150px; font-size: 14px; font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif; font-weight: 600">Measure:</a>
            <el-select v-model="value1" placeholder="Select" style="width: 200px; margin-left: 10px;">
                <el-option v-for="item in options1" :key="item.value" :label="item.label" :value="item.value" />
            </el-select>
            <a
                style="margin-left: 20px; font-size: 14px; font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif; font-weight: 600">Group
                by:</a>
            <el-select v-model="value2" placeholder="Select" style="width: 200px; margin-left: 10px;">
                <el-option v-for="item in options2" :key="item.value" :label="item.label" :value="item.value" />
            </el-select>
            <a
                style="margin-left: 20px; font-size: 14px; font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif; font-weight: 600">Color
                by:</a>
            <el-select v-model="value3" placeholder="Select" style="width: 200px; margin-left: 10px;">
                <el-option v-for="item in options3" :key="item.value" :label="item.label" :value="item.value" />
            </el-select>
        </div>
        <div style="margin-top: 5px;">
            <el-row>
                <el-col :span="3" style="margin-left: 20px; margin-top: 28px;">
                    <div class="select-container">
                        <div class="select"
                            style="color: rgb(118,118,118); font-size: 14px; font-weight: 600; margin-left: 10px; margin-bottom: 3px;"
                            @click="selectAll">Select All
                        </div>
                        <div class="underline" :style="[visibility]"></div>
                    </div>
                    <div style="display: flex; align-items: center; margin-top: 15px;">
                        <div class="square" :style="[styles.unknown, clicked.unknown && styles.clicked]"
                            @click="handleClick('unknown')"></div>
                        <a style="font-size: 14px; margin-top: -3px; margin-left: 2px;">unknown</a>
                    </div>
                    <div style="display: flex; align-items: center; margin-top: 5px;">
                        <div class="square" :style="[styles.F2Pool, clicked.F2Pool && styles.clicked]"
                            @click="handleClick('F2Pool')">
                        </div>
                        <a style="font-size: 14px; margin-top: -3px; margin-left: 2px;">F2Pool</a>
                    </div>
                    <div style="display: flex; align-items: center; margin-top: 5px;">
                        <div class="square" :style="[styles.AntPool, clicked.AntPool && styles.clicked]"
                            @click="handleClick('AntPool')"></div>
                        <a style="font-size: 14px; margin-top: -3px; margin-left: 2px;">AntPool</a>
                    </div>
                    <div style="display: flex; align-items: center; margin-top: 5px;">
                        <div class="square" :style="[styles.BTCcom, clicked.BTCcom && styles.clicked]"
                            @click="handleClick('BTCcom')">
                        </div>
                        <a style="font-size: 14px; margin-top: -3px; margin-left: 2px;">BTC.com</a>
                    </div>
                    <div style="display: flex; align-items: center; margin-top: 5px;">
                        <div class="square" :style="[styles.SlushPool, clicked.SlushPool && styles.clicked]"
                            @click="handleClick('SlushPool')"></div>
                        <a style="font-size: 14px; margin-top: -3px; margin-left: 2px;">SlushPool</a>
                    </div>
                    <div style="display: flex; align-items: center; margin-top: 5px;">
                        <div class="square" :style="[styles.DeepBit, clicked.DeepBit && styles.clicked]"
                            @click="handleClick('DeepBit')"></div>
                        <a style="font-size: 14px; margin-top: -3px; margin-left: 2px;">DeepBit</a>
                    </div>
                    <div style="display: flex; align-items: center; margin-top: 5px;">
                        <div class="square" :style="[styles.BTCGuild, clicked.BTCGuild && styles.clicked]"
                            @click="handleClick('BTCGuild')"></div>
                        <a style="font-size: 14px; margin-top: -3px; margin-left: 2px;">BTC Guild</a>
                    </div>
                    <div style="display: flex; align-items: center; margin-top: 5px;">
                        <div class="square" :style="[styles.ViaBTC, clicked.ViaBTC && styles.clicked]"
                            @click="handleClick('ViaBTC')">
                        </div>
                        <a style="font-size: 14px; margin-top: -3px; margin-left: 2px;">ViaBTC</a>
                    </div>
                    <div style="display: flex; align-items: center; margin-top: 5px;">
                        <div class="square" :style="[styles.Poolin, clicked.Poolin && styles.clicked]"
                            @click="handleClick('Poolin')">
                        </div>
                        <a style="font-size: 14px; margin-top: -3px; margin-left: 2px;">Poolin</a>
                    </div>
                    <div style="display: flex; align-items: center; margin-top: 5px;">
                        <div class="square" :style="[styles.GHashIO, clicked.GHashIO && styles.clicked]"
                            @click="handleClick('GHashIO')"></div>
                        <a style="font-size: 14px; margin-top: -3px; margin-left: 2px;">GHash.IO</a>
                    </div>
                    <div style="display: flex; align-items: center; margin-top: 5px;">
                        <div class="square" :style="[styles.BitFury, clicked.BitFury && styles.clicked]"
                            @click="handleClick('BitFury')"></div>
                        <a style="font-size: 14px; margin-top: -3px; margin-left: 2px;">BitFury</a>
                    </div>
                    <div style="display: flex; align-items: center; margin-top: 5px;">
                        <div class="square" :style="[styles.others, clicked.others && styles.clicked]"
                            @click="handleClick('others')">
                        </div>
                        <a style="font-size: 14px; margin-top: -3px; margin-left: 2px;">others</a>
                    </div>
                </el-col>
                <el-col :span="20" style="margin-left: 20px; margin-top: -30px;">
                    <div id="chart" style="height: 480px; width: 106%;"></div>
                </el-col>
            </el-row>
        </div>
    </div>
</template>
<script setup>
import { ref, onMounted } from 'vue'
import * as echarts from 'echarts'

const clicked = ref({
    unknown: false,
    F2Pool: false,
    AntPool: false,
    BTCcom: false,
    SlushPool: false,
    DeepBit: false,
    BTCGuild: false,
    ViaBTC: false,
    Poolin: false,
    GHashIO: false,
    BitFury: false,
    others: false,
});
const styles = {
    unknown: {
        backgroundColor: 'rgb(102,102,102)',
        width: '10px',
        height: '10px',
    },
    F2Pool: {
        backgroundColor: 'rgb(31,119,180)',
        width: '10px',
        height: '10px',
    },
    AntPool: {
        backgroundColor: 'rgb(255,127,14)',
        width: '10px',
        height: '10px',
    },
    BTCcom: {
        backgroundColor: 'rgb(44,160,44)',
        width: '10px',
        height: '10px',
    },
    SlushPool: {
        backgroundColor: 'rgb(214,39,40)',
        width: '10px',
        height: '10px',
    },
    DeepBit: {
        backgroundColor: 'rgb(148,103,189)',
        width: '10px',
        height: '10px',
    },
    BTCGuild: {
        backgroundColor: 'rgb(140,86,75)',
        width: '10px',
        height: '10px',
    },
    ViaBTC: {
        backgroundColor: 'rgb(227,119,194)',
        width: '10px',
        height: '10px',
    },
    Poolin: {
        backgroundColor: 'rgb(166,118,29)',
        width: '10px',
        height: '10px',
    },
    GHashIO: {
        backgroundColor: 'rgb(188,189,34)',
        width: '10px',
        height: '10px',
    },
    BitFury: {
        backgroundColor: 'rgb(13,190,207)',
        width: '10px',
        height: '10px',
    },
    others: {
        backgroundColor: 'rgb(153,153,153)',
        width: '10px',
        height: '10px',
    },
    clicked: {
        opacity: 0.2,
    },
};

const handleClick = (key) => {
    clicked.value[key] = !clicked.value[key];
}
const visibility = ref('hidden')
const selectAll = () => {
    Object.keys(clicked.value).forEach(key => {
        if (clicked.value[key] == true) {
            clicked.value[key] = false
        }
    });
}

//     'Orange',
//     'Tomato',
//     'Apple',
//     'Sakana',
//     'Banana',
//     'Iwashi',
//     'Snappy Fish',
//     'Lemon',
//     'Pasta'
// ];
// const years = ['2001', '2002', '2003', '2004', '2005', '2006', '2007', '2008', '2009', '2010', 
//               '2011', '2012', '2013', '2014', '2015', '2016', '2017', '2018', '2019', '2020', 
//               '2021', '2022', '2023', '2024'];
// const shuffle = (array) => {
//     let currentIndex = array.length;
//     let randomIndex = 0;
//     while (currentIndex > 0) {
//         randomIndex = Math.floor(Math.random() * currentIndex);
//         currentIndex--;
//         [array[currentIndex], array[randomIndex]] = [
//             array[randomIndex],
//             array[currentIndex]
//         ];
//     }
//     return array;
// };
// const generateRankingData = () => {
//     const map = new Map();
//     const defaultRanking = Array.from({ length: names.length }, (_, i) => i + 1);
//     for (const year of years) {
//         console.log(year)
//         const shuffleArray = shuffle(defaultRanking);
//         names.forEach((name, i) => {
//             map.set(name, (map.get(name) || []).concat(shuffleArray[i]));
//         });
//     }
//     return map;
// };
// const generateSeriesList = () => {
//     const seriesList = [];
//     const rankingMap = generateRankingData();
//     rankingMap.forEach((data, name) => {
//         const series = {
//             name,
//             symbolSize: 20,
//             type: 'line',
//             smooth: true,
//             emphasis: {
//                 focus: 'series'
//             },
//             endLabel: {
//                 show: true,
//                 formatter: '{a}',
//                 distance: 20
//             },
//             lineStyle: {
//                 width: 4
//             },
//             data
//         };
//         seriesList.push(series);
//     });
//     return seriesList;
// };
// const myChart = ref(null);
// onMounted(() => {
//     const chartDom = document.getElementById('chart');
//     myChart.value = echarts.init(chartDom);
//     const option = {
//         tooltip: {
//             trigger: 'item'
//         },
//         grid: {
//             left: 30,
//             right: 110,
//             bottom: 30,
//             containLabel: true
//         },
//         toolbox: {
//             feature: {
//                 saveAsImage: {}
//             }
//         },
//         xAxis: {
//             type: 'category',
//             splitLine: {
//                 show: true
//             },
//             axisLabel: {
//                 margin: 30,
//                 fontSize: 16
//             },
//             boundaryGap: false,
//             data: years
//         },
//         yAxis: {
//             type: 'value',
//             axisLabel: {
//                 margin: 30,
//                 fontSize: 16,
//                 formatter: '#{value}'
//             },
//             inverse: true,
//             interval: 1,
//             min: 1,
//             max: names.length
//         },
//         series: generateSeriesList()
//     };
//     myChart.value.setOption(option);
// });

onMounted(() => {
    const chartDom = document.getElementById('chart');
    const myChart = echarts.init(chartDom);

    const rawData = [
        [100, 302, 301, 334, 390, 330, 320],
        [820, 832, 901, 934, 1290, 1330, 1320],
        [320, 132, 101, 134, 90, 230, 210],
        [220, 182, 191, 234, 290, 330, 310],
        [150, 212, 201, 154, 190, 330, 410],
        [220, 182, 191, 234, 290, 330, 310],
        [100, 302, 301, 334, 390, 330, 320],
        [100, 302, 301, 334, 390, 330, 320],
        [100, 302, 301, 334, 390, 330, 320],
        [100, 302, 301, 334, 390, 330, 320],
        [100, 302, 301, 334, 390, 330, 320],
        [100, 302, 301, 334, 390, 330, 320],
    ];

    // function transposeArray(array) {
    //     return array[0].map((_, colIndex) => array.map(row => row[colIndex]));
    // }

    // const transposedData = transposeArray(rawData);
    // const originalIndices = transposedData.map(column => {
    //     const indexedColumn = column.map((value, idx) => ({
    //         value: value,
    //         originalIndex: idx
    //     }));
    //     const sortedColumn = indexedColumn.slice().sort((b, a) => b.value - a.value);
    //     return sortedColumn.map(item => item.originalIndex);
    // });

    // const sortedColumns = transposedData.map((column, index) => {
    //     return {
    //         index: index,
    //         values: column.slice().sort((b, a) => b - a)
    //     };
    // });
    // const sortedTransposedData = sortedColumns.map(column => column.values);
    // const sortedRawData = transposeArray(sortedTransposedData);

    // const transposedOriginalIndices = transposeArray(originalIndices);

    const totalData = rawData[0].map((col, i) =>
        rawData.reduce((acc, row) => acc + row[i], 0)
    );

    // const seriesName = ['unknown', 'F2Pool', 'AntPool', 'BTCcom', 'SlushPool', 'DeepBit',
    //     'BTCGuild', 'ViaBTC', 'Poolin', 'GHashIO', 'BitFury', 'others'];

    const color = ['#666666', '#1F77B4', '#FF7F0E', '#2CA02C', '#D62728',
        '#9467BD', '#8C564B', '#E377C2', '#A6761D', '#BCBD22', '#0DBECF', '#999999'];
    const numDataPoints = rawData[0].length
    const barwidth = numDataPoints > 7 ? `${Math.floor(60 / numDataPoints)}%` : '60%'
    const series = [
        'unknown',
        'F2Pool',
        'AntPool',
        'BTCcom',
        'SlushPool',
        'DeepBit',
        'BTCGuild',
        'ViaBTC',
        'Poolin',
        'GHashIO',
        'BitFury',
        'others'
    ].map((name, sid) => {
        return {
            name,
            type: 'bar',
            stack: 'total',
            barWidth: barwidth,
            itemStyle: {
                color: color[sid]
            },
            data: rawData[sid].map((d, did) =>
                totalData[did] <= 0 ? 0 : d / totalData[did] * 100
            )
        };
    });

    const elements = [];
    const grid = { left: 95, top: 60, right: 95, bottom: 70 };
    const gridWidth = myChart.getWidth() - grid.left - grid.right;
    const gridHeight = myChart.getHeight() - grid.top - grid.bottom;
    const categoryWidth = gridWidth / rawData[0].length;
    const barWidth = categoryWidth * 0.6;
    const barPadding = (categoryWidth - barWidth) / 2;

    for (let j = 1, jlen = rawData[0].length; j < jlen; ++j) {
        const leftX = grid.left + categoryWidth * j - barPadding;
        const rightX = leftX + barPadding * 2;
        let leftY = grid.top + gridHeight;
        let rightY = leftY;
        for (let i = 0, len = series.length; i < len; ++i) {
            const points = [];
            const leftBarHeight = (rawData[i][j - 1] / totalData[j - 1]) * gridHeight;
            points.push([leftX, leftY]);
            points.push([leftX, leftY - leftBarHeight]);
            const rightBarHeight = (rawData[i][j] / totalData[j]) * gridHeight;
            points.push([rightX, rightY - rightBarHeight]);
            points.push([rightX, rightY]);
            points.push([leftX, leftY]);
            leftY -= leftBarHeight;
            rightY -= rightBarHeight;
            elements.push({
                type: 'polygon',
                shape: {
                    points
                },
                style: {
                    fill: color[i],
                    opacity: 0.25
                },

            });
        }
    }
    // const series = transposedOriginalIndices.map((row, idx) => {
    //     let name = [];
    //     let data = [];
    //     let colors = [];
    //     row.forEach((value, index) => {
    //         name.push(seriesName[value]);
    //         data.push(sortedRawData[idx][index] / totalData[index] * 100);
    //         colors.push(color[value]);
    //     });
    //     return {
    //         name: name.join(', '), 
    //         type: 'bar',
    //         barWidth: '60%',
    //         stack: 'total',
    //         label: {
    //             show: false
    //         },
    //         // itemStyle: {
    //         //     color: colors
    //         // },
    //         data: data
    //     };
    // });

    const option = {
        legend: {
            show: false
        },
        yAxis: {
            type: 'value',
            min: 0,
            max: 100,
            interval: 10
        },
        xAxis: {
            type: 'category',
            data: ['2018', '2019', '2020', '2021', '2022', '2023', '2024']
        },
        series,
        graphic: {
            elements
        },
    };

    myChart.setOption(option);
});

const value1 = ref(1)
const value2 = ref(1)
const value3 = ref(1)
const options1 = [
    {
        label: "Market share(%)",
        value: 1
    },
    {
        label: "Hash rate(TH/s)",
        value: 2
    },
    {
        label: "Electricity(GW)",
        value: 3
    },
    {
        label: "Total reward(BTC)",
        value: 4
    },
    {
        label: "Total reward(USD)",
        value: 5
    },
    {
        label: "Transaction fees(BTC)",
        value: 6
    },
    {
        label: "Transaction fees(USD)",
        value: 7
    },
]
const options2 = [
    {
        label: "Mining pool",
        value: 1
    },
    {
        label: "Payout scheme",
        value: 2
    },
    {
        label: "Location",
        value: 3
    },
]
const options3 = [
    {
        label: "Mining pool",
        value: 1
    },
    {
        label: "Payout scheme",
        value: 2
    },
    {
        label: "Location",
        value: 3
    },
]

</script>
<style>
.select {
    cursor: pointer;
}

.underline {
    width: 80px;
    height: 3px;
    background-color: rgb(118, 118, 118);
    visibility: hidden;
    /* 初始隐藏 */
    margin-left: 3px;
}

.select-container:hover .underline {
    visibility: visible;
    /* 鼠标悬停时显示 */
}

.square {
    cursor: pointer;
}
</style>