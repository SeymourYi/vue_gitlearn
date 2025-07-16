<template>
  <div v-for="(item, idx) in mapdata" :key="item.indicatorName">
    <div :ref="el => mapRefs[idx] = el as Element" 
      :style="{width: '400px', height: '300px'}"></div>
  </div>
</template>
<script setup lang="ts">
import { ref, onMounted, nextTick, computed } from 'vue';
import * as echarts from 'echarts';
const mapdata = ref([
    {
        "indicatorLists": [
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "再灌注率"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "再灌注例数"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "患者例数"
                    }
                ],
                "indicatorTime": "2025年01月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "再灌注率"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "再灌注例数"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "患者例数"
                    }
                ],
                "indicatorTime": "2025年02月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "再灌注率"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "再灌注例数"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "患者例数"
                    }
                ],
                "indicatorTime": "2025年03月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "再灌注率"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "再灌注例数"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "患者例数"
                    }
                ],
                "indicatorTime": "2025年04月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "再灌注率"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "再灌注例数"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "患者例数"
                    }
                ],
                "indicatorTime": "2025年05月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "再灌注率"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "再灌注例数"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "患者例数"
                    }
                ],
                "indicatorTime": "2025年06月"
            }
        ],
        "indicatorName": "发病至首次医疗接触在24小时以内的STEMI患者再灌注率(包括溶栓后介入)"
    },
    {
        "indicatorLists": [
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "ACS患者介入总例数"
                    },
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "死亡率"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "死亡例数"
                    }
                ],
                "indicatorTime": "2025年01月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "ACS患者介入总例数"
                    },
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "死亡率"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "死亡例数"
                    }
                ],
                "indicatorTime": "2025年02月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "ACS患者介入总例数"
                    },
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "死亡率"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "死亡例数"
                    }
                ],
                "indicatorTime": "2025年03月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "ACS患者介入总例数"
                    },
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "死亡率"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "死亡例数"
                    }
                ],
                "indicatorTime": "2025年04月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "ACS患者介入总例数"
                    },
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "死亡率"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "死亡例数"
                    }
                ],
                "indicatorTime": "2025年05月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "ACS患者介入总例数"
                    },
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "死亡率"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "死亡例数"
                    }
                ],
                "indicatorTime": "2025年06月"
            }
        ],
        "indicatorName": "ACS介入患者的死亡率"
    },
    {
        "indicatorLists": [
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "再灌注率"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "患者例数"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "再灌注例数"
                    }
                ],
                "indicatorTime": "2025年01月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "再灌注率"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "患者例数"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "再灌注例数"
                    }
                ],
                "indicatorTime": "2025年02月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "再灌注率"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "患者例数"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "再灌注例数"
                    }
                ],
                "indicatorTime": "2025年03月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "再灌注率"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "患者例数"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "再灌注例数"
                    }
                ],
                "indicatorTime": "2025年04月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "231",
                        "unit": "2",
                        "description": "再灌注率"
                    },
                    {
                        "value": "888",
                        "unit": "3",
                        "description": "患者例数"
                    },
                    {
                        "value": "168",
                        "unit": "3",
                        "description": "再灌注例数"
                    }
                ],
                "indicatorTime": "2025年05月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "521",
                        "unit": "2",
                        "description": "再灌注率"
                    },
                    {
                        "value": "122",
                        "unit": "3",
                        "description": "患者例数"
                    },
                    {
                        "value": "332",
                        "unit": "3",
                        "description": "再灌注例数"
                    }
                ],
                "indicatorTime": "2025年06月"
            }
        ],
        "indicatorName": "发病至首次医疗接触在12小时以内的STEMI患者再灌注率"
    },
    {
        "indicatorLists": [
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "达标率"
                    },
                    {
                        "value": "0",
                        "unit": "1",
                        "description": "平均时间"
                    }
                ],
                "indicatorTime": "2025年01月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "达标率"
                    },
                    {
                        "value": "0",
                        "unit": "1",
                        "description": "平均时间"
                    }
                ],
                "indicatorTime": "2025年02月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "达标率"
                    },
                    {
                        "value": "0",
                        "unit": "1",
                        "description": "平均时间"
                    }
                ],
                "indicatorTime": "2025年03月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "达标率"
                    },
                    {
                        "value": "0",
                        "unit": "1",
                        "description": "平均时间"
                    }
                ],
                "indicatorTime": "2025年04月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "达标率"
                    },
                    {
                        "value": "0",
                        "unit": "1",
                        "description": "平均时间"
                    }
                ],
                "indicatorTime": "2025年05月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "达标率"
                    },
                    {
                        "value": "0",
                        "unit": "1",
                        "description": "平均时间"
                    }
                ],
                "indicatorTime": "2025年06月"
            }
        ],
        "indicatorName": "所有ACS患者从确诊到负荷量双抗给药时间(<10分钟)"
    },
    {
        "indicatorLists": [
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "患者例数"
                    },
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "达标率"
                    },
                    {
                        "value": "0",
                        "unit": "1",
                        "description": "平均D2N时间"
                    }
                ],
                "indicatorTime": "2025年01月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "患者例数"
                    },
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "达标率"
                    },
                    {
                        "value": "0",
                        "unit": "1",
                        "description": "平均D2N时间"
                    }
                ],
                "indicatorTime": "2025年02月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "患者例数"
                    },
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "达标率"
                    },
                    {
                        "value": "0",
                        "unit": "1",
                        "description": "平均D2N时间"
                    }
                ],
                "indicatorTime": "2025年03月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "患者例数"
                    },
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "达标率"
                    },
                    {
                        "value": "0",
                        "unit": "1",
                        "description": "平均D2N时间"
                    }
                ],
                "indicatorTime": "2025年04月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "患者例数"
                    },
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "达标率"
                    },
                    {
                        "value": "0",
                        "unit": "1",
                        "description": "平均D2N时间"
                    }
                ],
                "indicatorTime": "2025年05月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "患者例数"
                    },
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "达标率"
                    },
                    {
                        "value": "0",
                        "unit": "1",
                        "description": "平均D2N时间"
                    }
                ],
                "indicatorTime": "2025年06月"
            }
        ],
        "indicatorName": "对于接受溶栓治疗的STEMI患者,月平均入门-开始溶栓时间(D2N<30分钟)"
    },
    {
        "indicatorLists": [
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "1",
                        "description": "平均时间"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "患者例数"
                    },
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "达标率"
                    }
                ],
                "indicatorTime": "2025年01月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "1",
                        "description": "平均时间"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "患者例数"
                    },
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "达标率"
                    }
                ],
                "indicatorTime": "2025年02月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "1",
                        "description": "平均时间"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "患者例数"
                    },
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "达标率"
                    }
                ],
                "indicatorTime": "2025年03月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "1",
                        "description": "平均时间"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "患者例数"
                    },
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "达标率"
                    }
                ],
                "indicatorTime": "2025年04月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "1",
                        "description": "平均时间"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "患者例数"
                    },
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "达标率"
                    }
                ],
                "indicatorTime": "2025年05月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "1",
                        "description": "平均时间"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "患者例数"
                    },
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "达标率"
                    }
                ],
                "indicatorTime": "2025年06月"
            }
        ],
        "indicatorName": "对于转运PPCI治疗的患者door-in and door-out(入门到出门)的时间(DI-DO 小于30分钟)"
    },
    {
        "indicatorLists": [
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "患者例数"
                    },
                    {
                        "value": "0",
                        "unit": "1",
                        "description": "平均D2W时间"
                    },
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "达标率"
                    }
                ],
                "indicatorTime": "2025年01月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "患者例数"
                    },
                    {
                        "value": "0",
                        "unit": "1",
                        "description": "平均D2W时间"
                    },
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "达标率"
                    }
                ],
                "indicatorTime": "2025年02月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "患者例数"
                    },
                    {
                        "value": "0",
                        "unit": "1",
                        "description": "平均D2W时间"
                    },
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "达标率"
                    }
                ],
                "indicatorTime": "2025年03月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "患者例数"
                    },
                    {
                        "value": "0",
                        "unit": "1",
                        "description": "平均D2W时间"
                    },
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "达标率"
                    }
                ],
                "indicatorTime": "2025年04月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "患者例数"
                    },
                    {
                        "value": "0",
                        "unit": "1",
                        "description": "平均D2W时间"
                    },
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "达标率"
                    }
                ],
                "indicatorTime": "2025年05月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "患者例数"
                    },
                    {
                        "value": "0",
                        "unit": "1",
                        "description": "平均D2W时间"
                    },
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "达标率"
                    }
                ],
                "indicatorTime": "2025年06月"
            }
        ],
        "indicatorName": "对于接受PPCI治疗的STEMI患者,月平均入门-导丝通过时间(D2W<90分钟)"
    },
    {
        "indicatorLists": [
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "死亡率"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "死亡例数"
                    }
                ],
                "indicatorTime": "2025年01月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "死亡率"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "死亡例数"
                    }
                ],
                "indicatorTime": "2025年02月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "死亡率"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "死亡例数"
                    }
                ],
                "indicatorTime": "2025年03月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "死亡率"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "死亡例数"
                    }
                ],
                "indicatorTime": "2025年04月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "死亡率"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "死亡例数"
                    }
                ],
                "indicatorTime": "2025年05月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "死亡率"
                    },
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "死亡例数"
                    }
                ],
                "indicatorTime": "2025年06月"
            }
        ],
        "indicatorName": "NSTEMI患者的死亡率"
    },
    {
        "indicatorLists": [
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "死亡例数"
                    },
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "死亡率"
                    }
                ],
                "indicatorTime": "2025年01月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "死亡例数"
                    },
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "死亡率"
                    }
                ],
                "indicatorTime": "2025年02月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "死亡例数"
                    },
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "死亡率"
                    }
                ],
                "indicatorTime": "2025年03月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "死亡例数"
                    },
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "死亡率"
                    }
                ],
                "indicatorTime": "2025年04月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "死亡例数"
                    },
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "死亡率"
                    }
                ],
                "indicatorTime": "2025年05月"
            },
            {
                "indicatorDataList": [
                    {
                        "value": "0",
                        "unit": "3",
                        "description": "死亡例数"
                    },
                    {
                        "value": "0",
                        "unit": "2",
                        "description": "死亡率"
                    }
                ],
                "indicatorTime": "2025年06月"
            }
        ],
        "indicatorName": "STEMI患者的死亡率"
    }
]
);
const seriesData = ref<any[]>([]);
computed(() => {
  return mapdata.value.map(() => null);
})
const colorPalette = ['#5470C6', '#91CC75', '#FAC858', '#EE6666', '#73C0DE', '#3BA272', '#FC8452', '#9A60B4']
      const innervalue = ref<string[][]>([]);
const innername = ref<string[][]>([]);
const innerunit = ref<string[][]>([]);
// 用于存储每个图表的 DOM 元素引用
const mapRefs = ref<(Element | null)[]>([]);

const unitMap = {
  '1': '分钟',
  '2': '%',
  '3': '例'
} as const;
type UnitKey = keyof typeof unitMap;

onMounted(async () => {
  await nextTick();
  mapdata.value.forEach((item, idx) => {
    const el = mapRefs.value[idx];
    if (el instanceof HTMLElement) {
      const chart = echarts.init(el);
      // 简单示例：每个图表显示 indicatorLists 的 value
      //x轴日期
      const indicator_date = item.indicatorLists.map(i => i.indicatorTime);
      //每一个表包含的数据所有项目
      const innerDataList = item.indicatorLists;
      //确定每个图表有几个指标数据项

      //由于每一个每个innerDataList对应一个图表，有几条数据项也是相同
        //所以这里仅仅判断第一项
      for (let index = 0; index < innerDataList[0].indicatorDataList.length; index++) {
        innervalue.value[index] = innerDataList.map(list => {
          return list.indicatorDataList[index].value; // ✅ 显式返回
        });
        innername.value[index] = innerDataList.map(list => {
          return list.indicatorDataList[index].description; // ✅ 显式返回
        });
        innerunit.value[index] = innerDataList.map(list => {  
          const unit = list.indicatorDataList[index].unit;
          return unit in unitMap ? unitMap[unit as UnitKey] : '未知单位'; // ✅ 显式返回
        });

        seriesData.value.push(
          {
            name: innername.value[index][0], // 使用第一个指标的描述作为名称
            data: innervalue.value[index],
            type:index % 2 === 0 ?  'bar' : 'line', // 偶数索引为柱状图，奇数索引为折线图
            itemStyle: {
              color: colorPalette[index % colorPalette.length] // 循环使用颜色数组
            }
          }
        )
      }
      // // 每个x轴对应的指标数据（value） 柱状图1_value
      // const innervalue_0 = innerDataList.map(list => {
      //   return list.indicatorDataList[0].value; // ✅ 显式返回
      // });
      // // 每个x轴对应的指标数据（value）柱状图1_描述
      // const innername_0 = innerDataList.map(list => {
      //   return list.indicatorDataList[0].description; // ✅ 显式返回
      // });
      // // 每个x轴对应的指标数据（value）柱状图1_单位
      // const innerunit_0 = innerDataList.map(list => {
      //   const unit = list.indicatorDataList[0].unit;
      //   return unit in unitMap ? unitMap[unit as UnitKey] : '未知单位';
      // });
      console.log(item)
     


      
        //由于每一个每个innerDataList对应一个图表，有几条数据项也是相同
        //所以这里仅仅判断第一项
        // if (innerDataList[0].indicatorDataList.length>1) {
        //   seriesData.value=[];
        //   // 处理多个数据项的情况
        //   seriesData.value.push({
        //     name: innername_0[0],
        //     data: innervalue_0,
        //     type: 'bar',
        //     itemStyle: {
        //       color: '#5470C6'
        //     }
        //   },
        //   {
        //       name: innername_0[0],
        //     data: innervalue_0,
        //     type: 'bar',
        //     itemStyle: {
        //       color: '#91CC75'
        //     }},
        //     { name: innername_0[0],
        //     data: innervalue_0,
        //     type: 'line',
        //     itemStyle: {
        //       color: '#FAC858'
        //     }});
      
        // }else if(innerDataList[0].indicatorDataList.length>0) {
        //   seriesData.value = [];
        //   seriesData.value.push({
        //     name: innername_0[0],
        //     data: innervalue_0,
        //     type: 'bar',
        //     itemStyle: {
        //       color: '#5470C6'
        //     }
        //   }, { name: innername_0[0],
        //     data: innervalue_0,
        //     type: 'line',
        //     itemStyle: {
        //       color: '#FAC858'
        //     }});
        // } else {
        //   seriesData.value = [];
        //   seriesData.value.push({
        //     name: innername_0[0],
        //     data: innervalue_0,
        //     type: 'bar',
        //     itemStyle: {
        //       color: '#5470C6'
        //     }
        //   });
        // }
      chart.setOption({
        title: {
          text: item.indicatorName,left: 'center', top: 10, textStyle: { fontSize: 12 }
        },
        tooltip: {},
        xAxis: { type: 'category', data: indicator_date},
        yAxis: { type: 'value' },
        series: seriesData.value
      });
      seriesData.value=[];
    }
  });
});
</script>

<style scoped>

</style>