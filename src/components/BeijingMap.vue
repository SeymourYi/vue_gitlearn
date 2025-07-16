<template>
  <div class="beijing-chart-container" ref="chartContainer"></div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import * as echarts from 'echarts';

const chartContainer = ref(null);
let chart = null;

onMounted(async () => {
  console.log('BeijingMap组件已挂载');
  await loadBeijingMap();
  initChart();
});

onUnmounted(() => {
  if (chart) {
    chart.dispose();
  }
});

// 加载北京地图数据
const loadBeijingMap = async () => {
  try {
    // 如果echarts已经注册了北京地图数据，则不需要重复加载
    if (!echarts.getMap('beijing')) {
      const response = await fetch('https://geo.datav.aliyun.com/areas_v3/bound/110000_full.json');
      const beijingJson = await response.json();
      echarts.registerMap('beijing', beijingJson);
    }
  } catch (error) {
    console.error('加载北京地图数据失败:', error);
  }
};

const initChart = () => {
  if (!chartContainer.value) {
    console.error('图表容器未找到');
    return;
  }
  
  // 初始化图表
  chart = echarts.init(chartContainer.value);
  
  // 北京地图配置
  const option = {
    title: {
      text: '北京市各区指数',
      left: 'center',
      top: 10
    },
    tooltip: {
      trigger: 'item',
      formatter: '{b}: {c}'
    },
    visualMap: {
      min: 10,
      max: 100,
      text: ['高', '低'],
      realtime: false,
      calculable: true,
      inRange: {
        color: ['#e0f3f8', '#43a2ca', '#0868ac']
      }
    },
    series: [
      {
        name: '北京',
        type: 'map',
        map: 'beijing',
        roam: true,
        emphasis: {
          label: {
            show: true
          }
        },
        data: [
          {name: '东城区', value: 98},
          {name: '西城区', value: 89},
          {name: '朝阳区', value: 76},
          {name: '丰台区', value: 63},
          {name: '石景山区', value: 55},
          {name: '海淀区', value: 82},
          {name: '门头沟区', value: 35},
          {name: '房山区', value: 29},
          {name: '通州区', value: 47},
          {name: '顺义区', value: 42},
          {name: '昌平区', value: 51},
          {name: '大兴区', value: 38},
          {name: '怀柔区', value: 25},
          {name: '平谷区', value: 19},
          {name: '密云区', value: 15},
          {name: '延庆区', value: 10}
        ]
      }
    ]
  };
  
  chart.setOption(option);
  
  // 监听窗口大小变化
  window.addEventListener('resize', () => {
    if (chart) {
      chart.resize();
    }
  });
};
</script>

<style scoped>
.beijing-chart-container {
  width: 100%;
  height: 100%;
}
</style> 