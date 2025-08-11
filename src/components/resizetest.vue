<template>
    <div class="chart-container">
      <h2>简单的ECharts图表（适配不同屏幕的大小）</h2>
      <div ref="chartRef" class="chart-wrapper"></div>
    </div>
  </template>
  
  <script setup lang="ts">
  import { ref, onMounted, onUnmounted } from 'vue'
  import * as echarts from 'echarts'
  
  const chartRef = ref<HTMLDivElement>()
  let myChart: echarts.ECharts | null = null
  let resizeTimer: number | null = null
  
  // 防抖的resize处理函数
  const handleResize = () => {
    if (resizeTimer) {
      clearTimeout(resizeTimer)
    }
    resizeTimer = window.setTimeout(() => {
      if (myChart) {
        myChart.resize()
      }
    }, 100)
  }
  
  onMounted(() => {
    if (chartRef.value) {
      // 初始化echarts实例
      myChart = echarts.init(chartRef.value)
      
      // 配置选项
      const option = {
        title: {
          text: '简单柱状图示例'
        },
        tooltip: {},
        xAxis: {
          data: ['衬衫', '羊毛衫', '雪纺衫', '裤子', '高跟鞋', '袜子']
        },
        yAxis: {},
        series: [
          {
            name: '销量',
            type: 'bar',
            data: [5, 20, 36, 10, 10, 20]
          }
        ]
      }
      
      // 使用刚指定的配置项和数据显示图表
      myChart.setOption(option)
      
      // 添加响应式调整图表大小的事件监听器
      window.addEventListener('resize', 
      handleResize
    )
    }
  })
  
  // 组件卸载时清理事件监听器和定时器
  onUnmounted(() => {
    if (resizeTimer) {
      clearTimeout(resizeTimer)
    }
    window.removeEventListener('resize', handleResize)
    if (myChart) {
      myChart.dispose()
    }
  })
  </script>
  
  <style scoped>
  .chart-container {
    width: 100%;
    height: 100vh;
    display: flex;
    flex-direction: column;
    padding: 20px;
    box-sizing: border-box;
  }
  
  h2 {
    text-align: center;
    color: #333;
    margin-bottom: 20px;
    flex-shrink: 0;
  }
  
  .chart-wrapper {
    flex: 1;
    width: 100%;
    min-height: 400px;
  }
  </style>
  