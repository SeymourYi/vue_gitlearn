<template>
    <div>
     acs数据大屏
   <div class="table-container">
   <div class="table-left">
    <div class="table-left-one">
        <div style="width: 100%; height: 400px;"
         ref="chartRef" class="table-left-one-one" 
         id="table-left-one-one">
        </div>
    </div>
    <div class="table-left-two">
    </div>
    <div class="table-left-three">123</div>
   </div>
   <div class="table-center">123</div>
   <div class="table-right">123</div>
   </div>
</div>
</template>

<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from 'vue';
import * as echarts from 'echarts';
const chartRef=ref<HTMLHtmlElement>()
let mychart:echarts.ECharts 
const initmychart=()=>{
    mychart=echarts.init(chartRef.value)
    const mychartoption={
     xAxis:{
        type:'category',
        data:['周一','周二','周三','周四','周五']
     },
     yAxis:{
        type:'value',
     },
     series:{
        name:'销量',
        type:'line',
        data:[120,222,333,401,50]
     },
     tooltip:{},
     title:{
        text:'213'
     }
    }
    mychart.setOption(mychartoption)   
}
onMounted(()=>{
    initmychart()
})
onBeforeUnmount(()=>{
    if (mychart!=null) {
          mychart.dispose()
    }
})

</script>


<style scoped>
.table-container{
    display: flex;
    flex-direction: row;
    align-items: center;
    width: 100%;
    height: 100%;
}   
.table-left{
    width: 20%;
    height: 100%;
    background-color: #ffffff;
    border: 1px solid brown;
}
.table-center{
    width: 60%;
    height: 100%;
    background-color: #ffffff;
    border: 1px solid brown;
}   
.table-right{
    width: 20%;
    height: 100%;
    background-color: #ffffff;
    border: 1px solid brown;
}
.table-left-one{
    width: 100%;
    height: 100%;
    background-color: #ffffff;
    border: 1px solid brown;
}
.table-left-two{
    width: 100%;
    height: 100%;
    background-color: #ffffff;
    border: 1px solid brown;
}
.table-left-three{
    width: 100%;
    height: 100%;
    background-color: #ffffff;
    border: 1px solid brown;
}
</style>