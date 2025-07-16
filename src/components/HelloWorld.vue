<script setup lang="ts">
import { ref, onMounted } from 'vue'
import * as echarts from 'echarts'

defineProps<{ msg: string }>()
const myshangqiuChart = ref(null);
const mybarChart = ref(null)
const mylineChart =ref(null)
const mymapChart = ref(null)
const setbeijingtmap = async() => {
  const response = await fetch('https://geo.datav.aliyun.com/areas_v3/bound/110000_full.json');
  const beijingJson = await response.json();
  echarts.registerMap('beijing', beijingJson);
}
const setshangqiumap =async () => {
  const response = await fetch('https://geo.datav.aliyun.com/areas_v3/bound/411400_full.json');
  const shangqiuJson = await response.json();
  echarts.registerMap('shangqiu', shangqiuJson);
}
onMounted(async() => {
  await setbeijingtmap();
  await setshangqiumap();
  const shangqiumapChart = echarts.init(myshangqiuChart.value);
  const mapChart = echarts.init(mymapChart.value);
  const barChart = echarts.init(mybarChart.value);
  const lineChart = echarts.init(mylineChart.value);
    barChart.setOption({
      title: {
        text: '柱状图'
      },
      tooltip:{},
      xAxis: {
        data: ['周五', '周六', '周日']
      },
      yAxis: {},
      series: [{
        data: ["23", "22", "12"],
        type: 'bar'
      }]
    })
    lineChart.setOption({
      title: {
        text:'折线图'
      },
      xAxis: {
     data:["周五","周六","周日"]
      },
      yAxis: {
        
      },
      series: [{
        data: [23, 33, 22],
        type:'line'
      }],
      tooltip: {
         
      }
    })
    await mapChart.setOption({
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
    })
    await shangqiumapChart.setOption({
    title: { 
      text: '商丘市各区县指数', 
      left: 'center',
      top: 10
    },
    tooltip: {
      trigger: 'item',
      formatter: '{b}: {c}'
    },
    visualMap: {
      min: 0,
      max: 100,
      text: ['高', '低'],
      realtime: false,
      calculable: true,
      inRange: {
        color: ['#e0f3f8', '#43a2ca', '#0868ac']
      }
    },
    series: [{
      name: '商丘',
      type: 'map',
      map: 'shangqiu',
      roam: true,
      emphasis: {
        label: {
          show: true
        }
      },
      data: [
        {name: '梁园区', value: 85},
        {name: '睢阳区', value: 78},
        {name: '永城市', value: 92},
        {name: '民权县', value: 65},
        {name: '睢县', value: 58},
        {name: '宁陵县', value: 52},
        {name: '柘城县', value: 48},
        {name: '虞城县', value: 62},
        {name: '夏邑县', value: 55}
      ]
    }]
  })
})
</script>

<template>

  <div class="charts-container">
    <div ref="mybarChart" id="barChart" class="chart"></div>
    <div ref="mylineChart" id="barChart" class="chart"></div>
    <div ref="mymapChart" id="barChart" class="chart"></div>
    <div ref="myshangqiuChart" id="barChart" class="chart"></div>
  </div>

  <p class="tips">这是使用ECharts实现的各种图表示例</p>
</template>

<style scoped>
.charts-container {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 20px;
  margin-top: 20px;
}

.chart {
  height: 300px;
  border: 1px solid #eee;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.tips {
  margin-top: 20px;
  color: #888;
  text-align: center;
}

@media (max-width: 768px) {
  .charts-container {
    grid-template-columns: 1fr;
  }
}
</style>
