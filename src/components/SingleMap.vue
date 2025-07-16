<template>
  <div class="chart-container">
    <div ref="chartRef" class="echart" style="width: 100%; height: 400px;"></div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'

import * as echarts from 'echarts'

const chartRef = ref<HTMLDivElement | null>(null)

onMounted(() => {
  if (chartRef.value) {
    const myChart = echarts.init(chartRef.value)
    const option = {
      title: {
        text: 'ECharts 示例'
      },
      tooltip: {
        trigger: 'axis'
      },
      legend: {
        data: ['实线折线', '虚线折线', '柱形A', '柱形B']
      },
      xAxis: {
        type: 'category',
        data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
      },
      yAxis: {
        type: 'value'
      },
      series: [
        {
          name: '实线折线',
          type: 'line',
          data: [120, 132, 101, 134, 90, 230, 210],
          lineStyle: {
            type: 'solid',
            width: 2
          }
        },
        {
          name: '虚线折线',
          type: 'line',
          data: [220, 182, 191, 234, 290, 330, 310],
          lineStyle: {
            type: 'dashed',
            width: 2
          }
        },
        {
          name: '柱形A',
          type: 'bar',
          data: [150, 232, 201, 154, 190, 330, 410],
          itemStyle: {
            color: '#5470C6'
          }
        },
        {
          name: '柱形B',
          type: 'bar',
          data: [98, 77, 101, 99, 40, 120, 150],
          itemStyle: {
            color: '#91CC75'
          }
        }
      ]
    }
    myChart.setOption(option)
  }
})
</script>

<style scoped>
.chart-container {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
.echart {
  min-width: 300px;
  min-height: 300px;
}
</style>