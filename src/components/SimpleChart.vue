<template>
    <div>
        <h2>简单柱状图（固定大小）</h2>
        <div ref="chartRef" style="width: 600px; height: 400px;"></div>
    </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'
import * as echarts from 'echarts'

const chartRef = ref<HTMLDivElement>()
let myChart: echarts.ECharts | null = null

onMounted(() => {
    if (chartRef.value) {
        // 初始化图表
        myChart = echarts.init(chartRef.value)
        
        // 配置选项
        const option = {
            title: {
                text: '简单示例'
            },
            tooltip: {},
            xAxis: {
                data: ['衬衫', '羊毛衫', '雪纺衫', '裤子', '高跟鞋', '袜子']
            },
            yAxis: {},
            series: [{
                name: '销量',
                type: 'bar',
                data: [5, 20, 36, 10, 10, 20]
            }]
        }
        
        // 使用配置项显示图表
        myChart.setOption(option)
    }
})

onUnmounted(() => {
    if (myChart) {
        myChart.dispose()
        myChart = null
    }
})
</script>

<style scoped>
h2 {
    color: #333;
    margin-bottom: 20px;
}
</style>