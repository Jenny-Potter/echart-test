<template>
  <div class="echarts-wrap">
    <mpvue-echarts :echarts="echarts" :onInit="initChart" canvasId="demo-canvas" />
  </div>
</template>

<script>
// import echarts from 'echarts'
import mpvueEcharts from 'mpvue-echarts'
import * as echarts from 'echarts/lib/echarts'
import 'echarts/lib/chart/bar'
import 'echarts/lib/component/tooltip'
import 'echarts/lib/component/legend'
import 'echarts/lib/component/grid'

let chart = null

export default {
  components: {
    mpvueEcharts
  },
  data () {
    return {
      echarts,
      option: {},
      dataTest: ['衬衫', '羊毛衫', '雪纺衫', '裤子', '高跟鞋', '袜子']
    }
  },
  methods: {
    setOption () {
      this.option = {
        tooltip: {},
        legend: {
          data: ['销量', '次数']
        },
        grid: {
          left: 100
        },
        xAxis: {
          data: this.dataTest
        },
        yAxis: [
          {
            type: 'value',
            name: '人数',
            axisLabel: {
              formatter: '{value}人'
            }
          },
          {
            type: 'value',
            name: '次数',
            axisLabel: {
              formatter: '{value}次'
            }
          }
        ],
        series: [
          {
            name: '销量',
            type: 'line',
            data: [6666, 20, 36, 10, 10, 100000000],
            lineStyle: {
              color: 'yellow'
            },
            hoverAnimation: true,
            itemStyle: {
              borderColor: 'green',
              emphasis: {
                borderColor: 'blue'
              }
            },
            yAxisIndex: 0
          },
          {
            name: '次数',
            type: 'line',
            data: [70, 45, 34, 23, 4, 5],
            lineStyle: {
              color: 'orange'
            },
            itemStyle: {
              borderColor: 'white'
            },
            yAxisIndex: 1
          }
        ]
      }
      return this.option
    },
    initChart (canvas, width, height) {
      chart = echarts.init(canvas, null, {
        width: width,
        height: height
      })
      canvas.setChart(chart)

      chart.setOption(this.setOption())
      this.onInit = chart

      return chart // 返回 chart 后可以自动绑定触摸操作
    }
  }
}
</script>

<style scoped>
.echarts-wrap {
  width: 100%;
  height: 200px;
  background: rgba(131, 153, 219, 0.4);
}
</style>