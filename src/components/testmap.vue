<template>
   <div>
    <div @click="goBack">返回</div>
   </div>
<div class="map-container">
    <div id="map"></div>
  </div>
</template>

<script setup lang="ts">
import { onMounted } from 'vue';
import * as echarts from 'echarts';
import { ElMessage } from 'element-plus';
import { v4 as uuidv4 } from 'uuid';
const goBack = () => {
  console.log('返回');
  switchMap('北京市', '110000');
}

const switchMap = async (name: string, code: string) => {
  const uuid = uuidv4();
 let response = await fetch(`https://geo.datav.aliyun.com/areas_v3/bound/${code}_full.json`);

if (!response.ok) {
  // 如果第一个失败，尝试第二个
  response = await fetch(`https://geo.datav.aliyun.com/areas_v3/bound/${code}.json`);
}

  const data = await response.json();
  echarts.registerMap(uuid, data);
  
  const chart = echarts.init(document.getElementById('map') as HTMLElement);
  const asd = [
    {
        "value": 20,
        "name": "东城区",
        "code": 110101
    },
    {
        "value": 20,
        "name": "西城区",
        "code": 110102
    },
    {
        "value": 20,
        "name": "朝阳区",
        "code": 110105
    },
    {
        "value": 20,
        "name": "丰台区",
        "code": 110106
    },
    {
        "value": 20,
        "name": "石景山区",
        "code": 110107
    },
    {
        "value": 20,
        "name": "海淀区",
        "code": 110108
    },
    {
        "value": 20,
        "name": "门头沟区",
        "code": 110109
    },
    {
        "value": 20,
        "name": "房山区",
        "code": 110111
    },
    {
        "value": 20,
        "name": "通州区",
        "code": 110112
    },
    {
        "value": 20,
        "name": "顺义区",
        "code": 110113
    },
    {
        "value": 20,
        "name": "昌平区",
        "code": 110114
    },
    {
        "value": 20,
        "name": "大兴区",
        "code": 110115
    },
    {
        "value": 20,
        "name": "怀柔区",
        "code": 110116
    },
    {
        "value": 20,
        "name": "平谷区",
        "code": 110117
    },
    {
        "value": 20,
        "name": "密云区",
        "code": 110118
    },
    {
        "value": 20,
        "name": "延庆区",
        "code": 110119
    }
]
  chart.setOption({
    title: {
      text: name + '地图',
      left: 'center'
    },
    tooltip: {
      trigger: 'item',
      formatter: (params: any) => {
        return `${params.name}: ${params.value || 0}`;
      }
    },
    visualMap: {
      min: 0,
      max: 120,
      left: 'left',
      top: 'bottom',
      text: ['高', '低'],
      textStyle: { color: '#fff' },
      inRange: {
        color: ['#90caf9', '#42a5f5', '#1976d2', '#0d47a1']
      }
    },
    series: [{
      type: 'map',
      map: uuid,
      data: asd,
      emphasis: {
        itemStyle: {
          areaColor: '#ff6b6b'
        }
      },
      itemStyle: {
        areaColor: '#e0f2fe',
        borderColor: '#fff',
        borderWidth: 1
      }
    }]
  });
}


onMounted(async () => {
  try {
    // 获取中国地图数据
    const response = await fetch('https://geo.datav.aliyun.com/areas_v3/bound/110000_full.json');
    const data = await response.json();
    const asd = [
    {
        "value": 20,
        "name": "东城区",
        "code": 110101
    },
    {
        "value": 20,
        "name": "西城区",
        "code": 110102
    },
    {
        "value": 20,
        "name": "朝阳区",
        "code": 110105
    },
    {
        "value": 20,
        "name": "丰台区",
        "code": 110106
    },
    {
        "value": 20,
        "name": "石景山区",
        "code": 110107
    },
    {
        "value": 20,
        "name": "海淀区",
        "code": 110108
    },
    {
        "value": 20,
        "name": "门头沟区",
        "code": 110109
    },
    {
        "value": 20,
        "name": "房山区",
        "code": 110111
    },
    {
        "value": 20,
        "name": "通州区",
        "code": 110112
    },
    {
        "value": 20,
        "name": "顺义区",
        "code": 110113
    },
    {
        "value": 20,
        "name": "昌平区",
        "code": 110114
    },
    {
        "value": 20,
        "name": "大兴区",
        "code": 110115
    },
    {
        "value": 20,
        "name": "怀柔区",
        "code": 110116
    },
    {
        "value": 20,
        "name": "平谷区",
        "code": 110117
    },
    {
        "value": 20,
        "name": "密云区",
        "code": 110118
    },
    {
        "value": 20,
        "name": "延庆区",
        "code": 110119
    }
]
    // 注册地图
    echarts.registerMap('mymap', data);
    const chart = echarts.init(document.getElementById('map') as HTMLElement);
    
    // 设置配置项
    chart.setOption({
      title: {
        text: '中国地图',
        left: 'center'
      },
  tooltip: {
      trigger: 'item',
      formatter: (params: any) => {
        return `${params.name}: ${params.value || 0}`;
      }
    },
          visualMap: {
      min: 0,
      max: 120,
      left: 'left',
      top: 'bottom',
      text: ['高', '低'],
      // calculable: true,
      textStyle: { color: '#fff' },
      inRange: {
        color: ['#90caf9', '#42a5f5', '#1976d2', '#0d47a1']
      }
    },
      series: [{
        type: 'map',
        map: 'mymap',
        // roam: true, // 允许缩放和平移
        data: asd,
        emphasis: {
          itemStyle: {
            areaColor: '#ff6b6b'
          }
        },
        itemStyle: {
          areaColor: '#e0f2fe',
          borderColor: '#fff',
          borderWidth: 1
        }
      }]
    });
    chart.on('click', (params: any) => {
      switchMap(params.data.name, params.data.code);
    });
    
    // 响应式处理
    window.addEventListener('resize', () => {
      chart.resize();
    });
    
  } catch (error) {
    console.error('加载地图失败:', error);
  }
});

</script>

<style scoped>
.map-container {
  width: 100%;
  height: 100vh;
}

#map {
  width: 100%;
  height: 100%;
}
</style>