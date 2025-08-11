<template>
  <div>
    <div>中国地图</div>
    <div ref="chartContainer" style="width: 100%; height: 500px;"></div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';
import * as echarts from 'echarts'; 

const chartContainer = ref<HTMLElement | null>(null)
let chartInstance: echarts.ECharts | null = null
const initChart = async() => {
  const mapDatajson=await fetch('https://geo.datav.aliyun.com/areas_v3/bound/110000_full.json').then(res => res.json());
  echarts.registerMap('beijing', mapDatajson);
  chartInstance = echarts.init(chartContainer.value as HTMLElement)
  chartInstance.setOption({
    title: {},
    tooltip: {
    },
    visualMap: {
      min: 10,
      max: 100,
      left: 'left',
      top: 'bottom',
      text: ['高','低'],
      inRange: {
        color: ['#e0ffff', '#006edd']
      },
      calculable: true
    },
    series: [{
      type: 'map',
      map: 'beijing',
      data: [
        {name: '东城区', value: 10, adcode: 110101},
        {name: '北京西城区', value: 15, adcode: 110102},
        {name: '北京朝阳区', value: 20, adcode: 110105},
        {name: '北京丰台区', value: 25, adcode: 110106},
        {name: '北京石景山区', value: 30, adcode: 110107},
        {name: '北京海淀区', value: 35, adcode: 110108},
        {name: '北京门头沟区', value: 40, adcode: 110109},
        {name: '北京房山区', value: 45, adcode: 110111},
        {name: '北京通州区', value: 50, adcode: 110112},
        {name: '北京顺义区', value: 55, adcode: 110113},
        {name: '北京昌平区', value: 60, adcode: 110114},
        {name: '北京大兴区', value: 65, adcode: 110115},
        {name: '北京怀柔区', value: 70, adcode: 110116},
        {name: '北京平谷区', value: 75, adcode: 110117},
        {name: '北京密云区', value: 80, adcode: 110118},
        {name: '北京延庆区', value: 85, adcode: 110119}
      ]
     }]
  })
  // 点击事件输出adcode
  chartInstance.on('click',  (params:any)=> {
    const data = params.data as any;
    if(data && data.adcode){
      console.log('区域编码:', data.adcode)
      // 你也可以用alert或emit等方式输出
    } else {
      // 点击空白区域，清除选中高亮
      chartInstance?.dispatchAction({
        type: 'downplay',
        seriesIndex: 0
      });
    }
  })
}
onMounted(() => {
  initChart();
});
</script>

<style scoped>
/* 推荐将样式写在这里，方便维护 */
</style>