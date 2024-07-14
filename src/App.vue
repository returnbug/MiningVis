<template>
  <div>
    <el-row class="row-bg" justify="space-around">
      <el-col :span="3">
        <el-image style="margin-left: -12px;" fit="cover" :src="url3"></el-image>
      </el-col>
      <el-col :span="16">
        <div class="ribbon1">
          <a style="margin-right: 12px; margin-top: 4px;">Time selection</a>
        </div>
        <div class="ribbon1-after">&nbsp;</div>
        <div class="time-select" style="height: 100px; margin-left: 24px; margin-top: -55px;">
          <TimeAxis />
        </div>
      </el-col>
      <el-col :span="4">
        <div>
          <el-image fit="cover" :src="url2" style="margin-top: 10px;"></el-image>
        </div>
        <div style="margin-top: 20px; margin-left: 15%">
          <el-button color="#D0D1D2" plain style="color:rgb(81, 81, 81);">
            <el-image style="height: 20px; width: 20px; margin-right: 5px;" fit="cover" :src="url"></el-image>
            Github
          </el-button>
          <el-button color="#D0D1D2" plain style="color:rgb(81, 81, 81);">
            <el-image style="height: 20px; width: 20px; margin-top: 3px; margin-right: 5px;" fit="cover"
              :src="url1"></el-image>
            Contact us
          </el-button>
        </div>
      </el-col>
    </el-row>
  </div>
  <div>
    <el-row>
      <el-col :span="16">
        <div>
          <div class="ribbon2">
            <a style="margin-right: 12px; margin-top: 4px;">Mining distribution</a>
          </div>
          <div class="ribbon2-after">&nbsp;</div>
          <div class="mining-distribution" style="height: 450px; margin-left: 24px; margin-top: -55px;">
            <MiningDistribution />
          </div>
        </div>
        <div>
          <div class="ribbon3">
            <a style="margin-right: 12px; margin-top: 4px;">Bitcoin news</a>
          </div>
          <div class="ribbon3-after">&nbsp;</div>
          <div class="bitcoin-news" style="height: 240px; margin-left: 24px; margin-top: -55px;">
            <BitcoinNews />
          </div>
        </div>
      </el-col>
      <el-col :span="8">
        <div>
          <div class="ribbon4">
            <a style="margin-right: 12px; margin-top: 4px;">{{ title }}</a>
          </div>
          <div class="ribbon4-after">&nbsp;</div>
          <div class="mining-pools"
            :style="{ height: miningPoolsHeight + 'px', marginLeft: '24px', marginTop: '-55px' }">
            <div style="margin-left: 100px">
              <el-radio-group v-model="radio" @change="handleRadioChange" fill="#f2f2f2" text-color="#000">
                <el-radio-button label="Mining pools" value="1" />
                <el-radio-button label="Bitcoin statistics" value="2" />
              </el-radio-group>
            </div>
          </div>
        </div>
        <div>
          <div class="ribbon5">
            <a style="margin-right: 12px; margin-top: 4px;">Cross pooling</a>
          </div>
          <div class="ribbon5-after">&nbsp;</div>
          <div class="cross-pooling"
            :style="{ height: crossPoolingHeight + 'px', marginLeft: '24px', marginTop: '-55px' }">
            <div style="display: flex; align-items: center;">
              <a
                style="margin-left: 100px; font-size: 14px; font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif; font-weight: 600">Measure:</a>
              <el-select v-model="value5" placeholder="Select" style="width: 200px; margin-left: 10px;">
                <el-option v-for="item in options5" :key="item.value" :label="item.label" :value="item.value" />
              </el-select>
              <el-button style="margin-left: auto;" color="#E0E1E2" @click="btn_5">{{ btn_5_text }}</el-button>
            </div>
            <CrossPooling v-show="showPool === 1" />
          </div>
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import github from '@/assets/image/github.png'
import email from '@/assets/image/email.png'
import logo from '@/assets/image/logo.jpg'
import ethereum from '@/assets/image/ethereum.png'
import TimeAxis from './components/TimeAxis.vue'
import CrossPooling from './components/CrossPooling.vue'
import MiningDistribution from './components/MiningDistribution.vue'
import BitcoinNews from './components/BitcoinNews.vue'

onMounted(() => {
  document.body.style.setProperty('--el-color-primary', '#038687');
  document.body.style.setProperty('--el-color-primary-light-9', '#e9f0f0');
  document.body.style.setProperty('--el-color-primary-light-3', '#1ba9aa');
})
const title = ref('Mining pools')
const radio = ref('1')
const crossPoolingHeight = ref(345)
const miningPoolsHeight = ref(345)
const isHidden = ref(false)
const btn_5_text = ref('Hide')
const url = ref(github)
const url1 = ref(email)
const url2 = ref(logo)
const url3 = ref(ethereum)
const value5 = ref(1)
let showPool = ref(1)
const options5 = [
  {
    label: 'Percent of cluters',
    value: 1
  },
  {
    label: 'Percent of total value',
    value: 2
  }
]

const btn_5 = () => {
  if (isHidden.value) {
    crossPoolingHeight.value = 345
    miningPoolsHeight.value -= 305
    btn_5_text.value = 'Hide'
    showPool = 1
  } else {
    crossPoolingHeight.value = 40
    miningPoolsHeight.value += 305
    btn_5_text.value = 'Show'
    showPool = 0
  }
  isHidden.value = !isHidden.value
}

const handleRadioChange = (value) => {
  if (value === '1') {
    title.value = 'Mining pools';
  } else if (value === '2') {
    title.value = 'Bitcoin statistics';
  }
};

</script>

<style scoped>
.ribbon1 {
  --f: 13px;
  --t: 10px;

  font-size: 13px;
  color: white;
  width: 130px;
  height: 28px;
  padding: 0 20px var(--f) calc(10px + var(--r));
  background: rgb(219, 40, 40);
  display: flex;
  justify-content: flex-end;
  text-align: right;
  border-top-right-radius: 5px;
  border-bottom-right-radius: 5px;
  margin-top: 20px;
  position: relative;
  z-index: 1;
}

.ribbon1-after {
  background: rgb(178, 30, 30);
  width: 14px;
  height: 14px;
  clip-path: polygon(0 0,
      100% 0,
      100% 100%,
      100% 100%);
}

.ribbon2 {
  --f: 13px;
  --t: 10px;

  font-size: 13px;
  color: white;
  width: 165px;
  height: 28px;
  padding: 0 20px var(--f) calc(10px + var(--r));
  background: rgb(242, 113, 28);
  display: flex;
  justify-content: flex-end;
  text-align: right;
  border-top-right-radius: 5px;
  border-bottom-right-radius: 5px;
  margin-top: 20px;
  position: relative;
  z-index: 1;
}

.ribbon2-after {
  background: rgb(207, 89, 12);
  width: 14px;
  height: 14px;
  clip-path: polygon(0 0,
      100% 0,
      100% 100%,
      100% 100%);
}

.ribbon3 {
  --f: 13px;
  --t: 10px;

  font-size: 13px;
  color: white;
  width: 120px;
  height: 28px;
  padding: 0 20px var(--f) calc(10px + var(--r));
  background: rgb(33, 186, 69);
  display: flex;
  justify-content: flex-end;
  text-align: right;
  border-top-right-radius: 5px;
  border-bottom-right-radius: 5px;
  margin-top: 20px;
  position: relative;
  z-index: 1;
}

.ribbon3-after {
  background: rgb(25, 143, 53);
  width: 14px;
  height: 14px;
  clip-path: polygon(0 0,
      100% 0,
      100% 100%,
      100% 100%);
}

.ribbon4 {
  --f: 13px;
  --t: 10px;

  font-size: 13px;
  color: white;
  width: 120px;
  height: 28px;
  padding: 0 20px var(--f) calc(10px + var(--r));
  background: rgb(33, 133, 208);
  display: flex;
  justify-content: flex-end;
  text-align: right;
  border-top-right-radius: 5px;
  border-bottom-right-radius: 5px;
  margin-top: 20px;
  position: relative;
  z-index: 1;
}

.ribbon4-after {
  background: rgb(26, 105, 164);
  width: 14px;
  height: 14px;
  clip-path: polygon(0 0,
      100% 0,
      100% 100%,
      100% 100%);
}

.ribbon5 {
  --f: 13px;
  --t: 10px;

  font-size: 13px;
  color: white;
  width: 120px;
  height: 28px;
  padding: 0 20px var(--f) calc(10px + var(--r));
  background: rgb(0, 181, 173);
  display: flex;
  justify-content: flex-end;
  text-align: right;
  border-top-right-radius: 5px;
  border-bottom-right-radius: 5px;
  margin-top: 20px;
  position: relative;
  z-index: 1;
}

.ribbon5-after {
  background: rgb(0, 130, 124);
  width: 14px;
  height: 14px;
  clip-path: polygon(0 0,
      100% 0,
      100% 100%,
      100% 100%);
}

.time-select {
  border: 1px solid #dededf;
  padding: 10px;
  border-radius: 4px;
  box-shadow: 0 4px 4px -2px rgba(0, 0, 0, 0.1),
    4px 0 4px -2px rgba(0, 0, 0, 0.1),
    -4px 0 4px -2px rgba(0, 0, 0, 0.1);
}

.mining-distribution,
.bitcoin-news,
.mining-pools,
.cross-pooling {
  border: 1px solid #dededf;
  padding: 10px;
  border-radius: 4px;
  box-shadow: 0 4px 4px -2px rgba(0, 0, 0, 0.1);
}

::v-deep .el-radio-button__inner {
  border: 2 !important;
  font-size: 12px;
  font-weight: 400;
  color: #696969;
  line-height: 14px;
}
</style>