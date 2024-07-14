<template>
    <div>
        <div style="display: flex; align-items: center;">
            <a
                style="margin-left: 100px; font-weight: 500; font-size: 14px; font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif; font-weight: 600">Search:</a>
            <el-input v-model="input" style="width: 240px; margin-left: 5px;" placeholder="Search..."
                :prefix-icon="Search" />
            <a
                style="margin-left: 20px; font-weight: 500; font-size: 14px; font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif; font-weight: 600">No.of
                news:</a>
            <el-slider v-model="num" style="width: 180px; margin-left: 15px; " :max="1000" />
            <a
                style="font-size: 15px; font-family:Cambria, Cochin, Georgia, Times, 'Times New Roman', serif; margin-top: -2px; margin-left: 15px;">{{
                    num }}</a>
            <div style="margin-top: -5px">
                <a
                    style="margin-left: 20px; font-size: 14px; font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif; font-weight: 600">Total
                    news:</a>
                <a
                    style="font-size: 15px; font-family:Cambria, Cochin, Georgia, Times, 'Times New Roman', serif; margin-top: 4px; margin-left: 2px;">{{
                        num1 }}</a>
                <a
                    style="margin-left: 10px; font-size: 14px; font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif; font-weight: 600">Display:</a>
                <a
                    style="font-size: 15px; font-family:Cambria, Cochin, Georgia, Times, 'Times New Roman', serif; margin-top: 4px; margin-left: 2px;">{{
                        num2 }}%</a>
            </div>
        </div>
        <div>
            <el-row>
                <el-col :span="5" style="margin-top: 15px; margin-left: 10px;">
                    <el-scrollbar class="custom-scrollbar" style="height: 200px; overflow-y: auto;" always>
                        <div class="select-container">
                            <div class="select"
                                style="color: rgb(118,118,118); font-size: 14px; font-weight: 600; margin-left: 10px; margin-bottom: 3px;"
                                @click="selectAll">Select All
                            </div>
                            <div class="underline" :style="[visibility]"></div>
                        </div>
                        <div>
                            <div style="display: flex; align-items: center; margin-top: 8px;">
                                <div class="square" :style="[styles.unknown, clicked.unknown && styles.clicked]"
                                    @click="handleClick('unknown')"></div>
                                <a
                                    style="font-size: 14px; margin-top: -3px; margin-left: 2px; font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif; font-weight: 600">Market
                                    Price</a>
                            </div>
                            <div style="font-size: 14px; color: rgb(74,74,74);">
                                bitcoinprice market price high watch hit new time volume trading
                            </div>
                        </div>
                        <div style="display: flex; align-items: center; margin-top: 20px;">
                            <div class="square" :style="[styles.F2Pool, clicked.F2Pool && styles.clicked]"
                                @click="handleClick('F2Pool')">
                            </div>
                            <a
                                style="font-size: 14px; margin-top: -3px; margin-left: 2px; font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif; font-weight: 600">Developers</a>
                        </div>
                        <div style="font-size: 14px; color: rgb(74,74,74);">
                            block fork network hard core <br>
                            size lightning new segwit2x segwit
                        </div>
                        <div style="display: flex; align-items: center; margin-top: 20px;">
                            <div class="square" :style="[styles.AntPool, clicked.AntPool && styles.clicked]"
                                @click="handleClick('AntPool')"></div>
                            <a
                                style="font-size: 14px; margin-top: -3px; margin-left: 2px; font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif; font-weight: 600">Regulations</a>
                        </div>
                        <div style="font-size: 14px; color: rgb(74,74,74);">
                            crypto cryptocurrency bank regulation tax ban government russia central exchange </div>
                        <div style="display: flex; align-items: center; margin-top: 20px;">
                            <div class="square" :style="[styles.BTCcom, clicked.BTCcom && styles.clicked]"
                                @click="handleClick('BTCcom')">
                            </div>
                            <a
                                style="font-size: 14px; margin-top: -3px; margin-left: 2px; font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif; font-weight: 600">Payments</a>
                        </div>
                        <div style="font-size: 14px; color: rgb(74,74,74);">
                            accept payment card btc buy pay debit service coinbase new </div>
                        <div style="display: flex; align-items: center; margin-top: 20px;">
                            <div class="square" :style="[styles.SlushPool, clicked.SlushPool && styles.clicked]"
                                @click="handleClick('SlushPool')"></div>
                            <a
                                style="font-size: 14px; margin-top: -3px; margin-left: 2px; font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif; font-weight: 600">Digital
                                currencies</a>
                        </div>
                        <div style="font-size: 14px; color: rgb(74,74,74);">
                            currency digital bank money virtual new central world video future </div>
                        <div style="display: flex; align-items: center; margin-top: 20px;">
                            <div class="square" :style="[styles.DeepBit, clicked.DeepBit && styles.clicked]"
                                @click="handleClick('DeepBit')"></div>
                            <a
                                style="font-size: 14px; margin-top: -3px; margin-left: 2px; font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif; font-weight: 600">Technical
                                analysis</a>
                        </div>
                        <div style="font-size: 14px; color: rgb(74,74,74);">
                            price analysis technical btc bitcoinprice bull market weekly term support </div>
                        <div style="display: flex; align-items: center; margin-top: 20px;">
                            <div class="square" :style="[styles.BTCGuild, clicked.BTCGuild && styles.clicked]"
                                @click="handleClick('BTCGuild')"></div>
                            <a
                                style="font-size: 14px; margin-top: -3px; margin-left: 2px; font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif; font-weight: 600">Hacking</a>
                        </div>
                        <div style="font-size: 14px; color: rgb(74,74,74);">
                            gox mt exchange hack user cd hacker attack btc steal </div>
                        <div style="display: flex; align-items: center; margin-top: 20px;">
                            <div class="square" :style="[styles.ViaBTC, clicked.ViaBTC && styles.clicked]"
                                @click="handleClick('ViaBTC')">
                            </div>
                            <a
                                style="font-size: 14px; margin-top: -3px; margin-left: 2px; font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif; font-weight: 600">Opinions</a>
                        </div>
                        <div style="font-size: 14px; color: rgb(74,74,74);">
                            say wall street crypto video ceo investor big buy bubble </div>
                        <div style="display: flex; align-items: center; margin-top: 20px;">
                            <div class="square" :style="[styles.Poolin, clicked.Poolin && styles.clicked]"
                                @click="handleClick('Poolin')">
                            </div>
                            <a
                                style="font-size: 14px; margin-top: -3px; margin-left: 2px; font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif; font-weight: 600">Interviews</a>
                        </div>
                        <div style="font-size: 14px; color: rgb(74,74,74);">
                            video interview audio ceo talk future btc founder andreas money </div>
                        <div style="display: flex; align-items: center; margin-top: 20px;">
                            <div class="square" :style="[styles.GHashIO, clicked.GHashIO && styles.clicked]"
                                @click="handleClick('GHashIO')"></div>
                            <a
                                style="font-size: 14px; margin-top: -3px; margin-left: 2px; font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif; font-weight: 600">Fintech</a>
                        </div>
                        <div style="font-size: 14px; color: rgb(74,74,74);">
                            cd startup bank technology tech new fintech payment launch join </div>
                        <div style="display: flex; align-items: center; margin-top: 20px;">
                            <div class="square" :style="[styles.BitFury, clicked.BitFury && styles.clicked]"
                                @click="handleClick('BitFury')"></div>
                            <a
                                style="font-size: 14px; margin-top: -3px; margin-left: 2px; font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif; font-weight: 600">Illegal
                                activities</a>
                        </div>
                        <div style="font-size: 14px; color: rgb(74,74,74);">
                            road silk money arrest drug us auction web btc dark </div>
                        <div style="display: flex; align-items: center; margin-top: 20px;">
                            <div class="square" :style="[styles.others, clicked.others && styles.clicked]"
                                @click="handleClick('others')">
                            </div>
                            <a
                                style="font-size: 14px; margin-top: -3px; margin-left: 2px; font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif; font-weight: 600">Wallets
                                and platforms</a>
                        </div>
                        <div style="font-size: 14px; color: rgb(74,74,74);">
                            wallet app new launch platform user mobile cryptocurrency ethereum payment </div>
                    </el-scrollbar>
                </el-col>
                <el-col :span="18" style="margin-left: 18px; position: relative;">
                    <div v-show="showNews" class="chart-news" :style="{ width: `${newsContent.length * 8}px` }">
                        <p style="padding-left: 13px;">{{ newsContent }}</p>
                    </div>
                    <div ref="chart"></div>
                </el-col>
            </el-row>
        </div>
    </div>
</template>
<script setup>
import { ref, onMounted } from 'vue'
import { Search } from '@element-plus/icons-vue'
import * as d3 from 'd3'

const input = ref('')
const num = ref(0)
const num1 = ref(0)
const num2 = ref(0)
const chart = ref(null)
const showNews = ref(false)
const newsContent = ref('')

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

const data = [
    { name: "Market Price", time: new Date("2020-01-01"), importance: 5 },
    { name: "Developers", time: new Date("2021-02-01"), importance: 8 },
    { name: "Regulations", time: new Date("2022-03-01"), importance: 3 },
    { name: "Payments", time: new Date("2023-04-01"), importance: 6 },
    { name: "Digital currencies", time: new Date("2024-05-01"), importance: 7 },
    { name: "Digital currencies", time: new Date("2025-05-01"), importance: 7 },
    { name: "Technical analysis", time: new Date("2020-06-01"), importance: 4 },
    { name: "Hacking", time: new Date("2021-07-01"), importance: 2 },
    { name: "Opinions", time: new Date("2022-08-01"), importance: 9 },
    { name: "Digital currencies", time: new Date("2023-05-01"), importance: 7 },
    { name: "Digital currencies", time: new Date("2024-05-01"), importance: 7 },
    { name: "Technical analysis", time: new Date("2025-06-01"), importance: 4 },
    { name: "Hacking", time: new Date("2020-07-01"), importance: 2 },
    { name: "Opinions", time: new Date("2021-08-01"), importance: 9 },
    { name: "Interviews", time: new Date("2022-09-01"), importance: 6 },
    { name: "Fintech", time: new Date("2023-10-01"), importance: 8 },
    { name: "Illegal activities", time: new Date("2024-11-01"), importance: 3 },
    { name: "Wallets and platforms", time: new Date("2025-12-01"), importance: 5 }
];

const colorMap = {
    "Market Price": "#666666",
    "Developers": "#1F77B4",
    "Regulations": "#FF7F0E",
    "Payments": "#2CA02C",
    "Digital currencies": "#D62728",
    "Technical analysis": "#9467BD",
    "Hacking": "#8C564B",
    "Opinions": "#E377C2",
    "Interviews": "#A6761D",
    "Fintech": "#BCBD22",
    "Illegal activities": "#0DBECF",
    "Wallets and platforms": "#999999"
};

const dodge = (data, { radius, x }) => {
    const circles = data.map(d => ({ x: x(d), y: 0, r: radius * d.importance / 10, data: d })).sort((a, b) => a.x - b.x);
    const epsilon = 1e-3;
    const padding = radius * 0;
    let head = null, tail = null;

    function intersects(x, y, r) {
        let a = head;
        while (a) {
            if (a.r + r - epsilon > Math.sqrt((a.x - x) ** 2 + (a.y - y) ** 2)) {
                return true;
            }
            a = a.next;
        }
        return false;
    }

    for (const b of circles) {
        let r = b.r + padding;

        while (head && head.x < b.x - r) head = head.next;

        if (intersects(b.x, b.y, r)) {
            let a = head;
            b.y = Infinity;
            do {
                let y1 = a.y + Math.sqrt((a.r + b.r) ** 2 - (a.x - b.x) ** 2);
                let y2 = a.y - Math.sqrt((a.r + b.r) ** 2 - (a.x - b.x) ** 2);
                if (Math.abs(y1) < Math.abs(b.y) && !intersects(b.x, y1, r)) b.y = y1;
                if (Math.abs(y2) < Math.abs(b.y) && !intersects(b.x, y2, r)) b.y = y2;
                a = a.next;
            } while (a);
        }

        b.next = null;
        if (head === null) head = tail = b;
        else tail = tail.next = b;
    }

    return circles;
};

const createChart = () => {
    const width = 928;
    const height = 230;
    const marginRight = 20;
    const marginLeft = 20;
    const marginBottom = 20;
    const radius = 5;
    const padding = 2;

    const timeFormat = d3.timeFormat("%Y-%m");

    const x = d3.scaleTime()
        .domain(d3.extent(data, d => d.time))
        .range([marginLeft, width - marginRight]);

    const svg = d3.select(chart.value)
        .append("svg")
        .attr("width", width)
        .attr("height", height)
        .attr("viewBox", [0, 0, width, height])
        .attr("style", "max-width: 100%; height: auto;");

    svg.append("g")
        .attr("transform", `translate(0,${height - marginBottom})`)
        .call(d3.axisBottom(x).tickFormat(timeFormat).tickSizeOuter(0));

    const circles = svg.append("g")
        .selectAll("circle")
        .data(dodge(data, { radius: radius * 2 + padding, x: d => x(d.time) }))
        .join("circle")
        .attr("cx", d => d.x)
        .attr("cy", d => height / 2 - radius - padding - d.y)
        .attr("r", d => d.r)
        .attr("fill", d => colorMap[d.data.name])
        .style("cursor", "pointer")
        .on("mouseover", function (d) {
            const data = d.srcElement.__data__.data
            showNews.value = true
            newsContent.value = `${data.name}, Date: ${timeFormat(data.time)}, Importance: ${data.importance}`
            d3.select(this)
                .style("stroke", "red")
                .style("stroke-width", 2);
        })
        .on("mouseout", function () {
            showNews.value = false;
            newsContent.value = '';
            d3.select(this)
                .style("stroke", "none");
        })
        .append("title")
        .text(d => d.data.name);

    circles.transition()
        .duration(1000) 
        .delay((i) => i * 100) 
        .attr("cx", d => d.x)
        .style("opacity", 1);
};

onMounted(() => {
    createChart()
});

</script>
<style scoped>
.el-slider::v-deep .el-slider__bar {
    background-color: #3399ff;
}

.el-slider::v-deep .el-slider__thumb {
    background-color: #3399ff;
    border-color: #3399ff;
}

.el-slider::v-deep .el-slider__button {
    border: 2px solid #3399ff;
}

.chart-news {
    font-size: 12px;
    position: absolute;
    top: 10px;
    left: 10px;
    width: calc(100% - 20px);
    height: 50px;
    border: 2px inset rgba(0, 0, 0, 1);
    background-color: white;
    z-index: 10;
}
</style>