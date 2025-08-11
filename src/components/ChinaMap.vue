<template>
  <div>
    <button v-if="currentLevel !== 'china'" @click="backToChina" class="back-btn">返回中国地图</button>
    <div class="china-map-container" ref="chartContainer"></div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue';
import * as echarts from 'echarts';
import { CENTERED_ALIGNMENT } from 'element-plus/es/components/virtual-list/src/defaults.mjs';

const chartContainer = ref<HTMLElement | null>(null);
let chartInstance: echarts.ECharts | null = null;

const currentLevel = ref<'china' | 'province'>('china');
const currentProvince = ref<{ name: string; adcode: string } | null>(null);

// 省份名称与adcode映射
const provinceList = [
  { name: '北京市', adcode: '110000', value: 98 },
  { name: '天津市', adcode: '120000', value: 85 },
  { name: '上海市', adcode: '310000', value: 96 },
  { name: '重庆市', adcode: '500000', value: 78 },
  { name: '河北省', adcode: '130000', value: 65 },
  { name: '河南省', adcode: '410000', value: 72 },
  { name: '云南省', adcode: '530000', value: 54 },
  { name: '辽宁省', adcode: '210000', value: 77 },
  { name: '黑龙江省', adcode: '230000', value: 68 },
  { name: '湖南省', adcode: '430000', value: 83 },
  { name: '安徽省', adcode: '340000', value: 75 },
  { name: '山东省', adcode: '370000', value: 88 },
  { name: '江苏省', adcode: '320000', value: 90 },
  { name: '浙江省', adcode: '330000', value: 92 },
  { name: '江西省', adcode: '360000', value: 70 },
  { name: '湖北省', adcode: '420000', value: 80 },
  { name: '广西壮族自治区', adcode: '450000', value: 67 },
  { name: '甘肃省', adcode: '620000', value: 58 },
  { name: '山西省', adcode: '140000', value: 63 },
  { name: '内蒙古自治区', adcode: '150000', value: 55 },
  { name: '陕西省', adcode: '610000', value: 76 },
  { name: '吉林省', adcode: '220000', value: 69 },
  { name: '福建省', adcode: '350000', value: 82 },
  { name: '贵州省', adcode: '520000', value: 60 },
  { name: '广东省', adcode: '440000', value: 95 },
  { name: '青海省', adcode: '630000', value: 45 },
  { name: '西藏自治区', adcode: '540000', value: 40 },
  { name: '四川省', adcode: '510000', value: 73 },
  { name: '宁夏回族自治区', adcode: '640000', value: 52 },
  { name: '海南省', adcode: '460000', value: 66 },
  { name: '台湾省', adcode: '710000', value: 79 },
  { name: '香港特别行政区', adcode: '810000', value: 93 },
  { name: '澳门特别行政区', adcode: '820000', value: 91 },
  { name: '新疆维吾尔自治区', adcode: '650000', value: 50 }
];

const provinceData = provinceList.map(({ name, value }) => ({ name, value }));

const initChart = async (mapType = 'china', mapDataUrl = 'https://geo.datav.aliyun.com/areas_v3/bound/100000_full.json', data = provinceData) => {
  if (!chartContainer.value) return;
  try {
    const mapData = await fetch(mapDataUrl).then(res => res.json());
    echarts.registerMap(mapType, mapData);
    if (!chartInstance) {
      chartInstance = echarts.init(chartContainer.value);
    }
    const option = {
      title: {
        text: mapType === 'china' ? '中国地图' : (currentProvince.value?.name || ''),
        left: 'center'
      },
      tooltip: {
        trigger: 'item',
        formatter: '{b}: {c}'
      },
      visualMap: {
        min: 0,
        max: 100,
        left: 'left',
        top: 'bottom',
        text: ['高', '低'],
        inRange: {
          color: ['#e0f7fa', '#4fc3f7', '#0288d1']
        },
        calculable: true
      },
      series: [
        {
          name: mapType === 'china' ? '中国' : (currentProvince.value?.name || ''),
          type: 'map',
          map: mapType,
          emphasis: {
            label: {
              show: true
            },
            itemStyle: {
              areaColor: '#ffd54f'
            }
          },
          data,
          universalTransition: true // 开启动画
        }
        
      ]
    };
    chartInstance.setOption(option);
    chartInstance.off('click');
    if (mapType === 'china') {
      chartInstance.on('click', handleProvinceClick);
    }
    window.addEventListener('resize', handleResize);
  } catch (error) {
    console.error('加载地图数据失败:', error);
  }
};

const handleProvinceClick = (params: any) => {
  const province = provinceList.find(p => p.name === params.name);
  if (!province) return;
  currentLevel.value = 'province';
  currentProvince.value = province;
  // 加载省级地图
  const url = `https://geo.datav.aliyun.com/areas_v3/bound/${province.adcode}_full.json`;
  loadProvinceMap(province.name, url);
};

const loadProvinceMap = async (mapType: string, mapDataUrl: string) => {
  await initChart(mapType, mapDataUrl, []); // 省级地图暂不显示数据
};

const backToChina = async () => {
  currentLevel.value = 'china';
  currentProvince.value = null;
  await initChart();
};

const handleResize = () => {
  chartInstance?.resize();
};

onMounted(() => {
  initChart();
});

onUnmounted(
  () => {
  if (chartInstance) {
    chartInstance.dispose();
    chartInstance = null;
  }
  window.removeEventListener('resize', handleResize);
}
);
</script>

<style scoped>
.china-map-container {
  width: 100%;
  height: 600px;
  margin: 0 auto;
}
.back-btn {
  margin: 10px 0 10px 10px;
  padding: 6px 16px;
  background: #1976d2;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
.back-btn:hover {
  background: #1565c0;
}
</style>