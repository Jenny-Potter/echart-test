<template>
  <div class="all-content">
    <ec-canvas id="mychart-dom-bar" :canva-id="'mychart-bar'" :ec="ec" />
  </div>
</template>
<script>
// import * as echarts from '../../static/ec-canvas/echarts'
// const initChart = function (canvas, width, height) {
//   const chart = echarts.init(canvas, null, {
//     width: width,
//     height: height
//   })
//   canvas.setChart(chart)
//   let option = {
//     title: {
//       text: 'ECharts 入门示例'
//     },
//     tooltip: {},
//     legend: {
//       data: ['销量']
//     },
//     xAxis: {
//       data: ['衬衫', '羊毛衫', '雪纺衫', '裤子', '高跟鞋', '袜子']
//     },
//     yAxis: {},
//     series: [{
//       name: '销量',
//       type: 'bar',
//       data: [5, 20, 36, 10, 10, 20]
//     }]
//   }

//   chart.setOption(option)
//   return chart
// }
export default {
  data () {
    return {
      ec: {
        // onInit: initChart
      }
    }
  }
}
</script>
<style scoped>
.all-content {
  background:#6666;
  width:100%
}
ec-canvas {
  width:100%;
  height:200px
}
#mychart-dom-bar {
  width:500px;
  height:500px
}
</style>