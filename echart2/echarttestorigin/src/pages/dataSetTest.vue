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
import 'echarts/lib/component/dataset'
import 'echarts/lib/component/dataZoom'

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
        legend: {},
        tooltip: {},
        dataZoom: [
          {
            type: 'slider',
            xAxisIndex: [0, 1],
            yAxisIndex: [0, 1],
            filterMode: 'filter',
            top: 220
          },
          {
            type: 'slider',
            xAxisIndex: 2,
            yAxisIndex: 2,
            filterMode: 'filter',
            start: 80,
            end: 100,
            top: 420
            // moveOnMouseWheel: true
          }
          // {
          //   type: 'inside',
          //   xAxisIndex: 2,
          //   yAxisIndex: 2,
          //   filterMode: 'filter',
          //   moveOnMouseWheel: true
          // }
          // {},
          // {}
        ],
        dataset: {
          // 提供一份数据。
          // sourceHeader: false,
          dimensions: ['time', '点赞数', '评论数', '收藏数'],
          source: [
            // ['fsdfsdfsdf', '2020-01-01', '2020-01-02', '2020-01-03'],
            // ['Matcha Latte', 43.3, 85.8, 93.7],
            // ['Milk Tea', 83.1, 73.4, 55.1],
            // ['Cheese Cocoa', 86.4, 65.2, 82.5],
            // ['Walnut Brownie', 72.4, 53.9, 39.1]
            // [43.3, 85.8, 93.7],
            // [83.1, 73.4, 55.1],
            // [86.4, 65.2, 82.5],
            // [72.4, 53.9, 39.1]
            ['01-01', 545, 23, 2],
            ['01-02', 345, 45, 22],
            ['01-03', 453, 6, 22],
            ['01-04', 3453, 234, 1],
            ['01-05', 345, 324, 324],
            ['01-06', 99, 34, 23],
            ['01-07', 999, 23, 23],
            ['01-08', 56, 12, 1],
            ['01-09', 4758, 124, 89],
            ['01-10', 123, 34, 23],
            ['01-12', 21313, 45, 668],
            ['01-13', 2173, 45, 668],
            ['01-14', 21313, 45, 668],
            ['01-15', 213131, 45, 668],
            ['01-16', 213113, 45, 668],
            ['01-17', 231313, 45, 668],
            ['01-18', 213313, 45, 668],
            ['01-19', 213313, 45, 668],
            ['01-20', 213313, 45, 668],
            ['01-21', 2131313, 45, 668]

            // {time: '2020-01-01', like: 545, comments: 23, collect: 22},
            // {time: '2020-01-02', like: 345, comments: 45, collect: 22},
            // {time: '2020-01-03', like: 453, comments: 56, collect: 22},
            // {time: '2020-01-04', like: 3453, comments: 78, collect: 1}
          ]
        },
        // 声明一个 X 轴，类目轴（category）。默认情况下，类目轴对应到 dataset 第一列。
        grid: [
          {top: 100, height: 100, right: 100, width: 150},
          {top: 200, height: 100, right: 100, width: 150},
          {top: 500, height: 100, right: 100, width: 150}
        ],
        xAxis: [
          {
            type: 'category',
            gridIndex: 0,
            boundaryGap: false
          },
          {
            type: 'category',
            gridIndex: 1,
            boundaryGap: false,
            min: function (value) { return value.min },
            max: 'dataMax'
          },
          {
            type: 'category',
            gridIndex: 2,
            boundaryGap: false
          }
        ],
        // 声明一个 Y 轴，数值轴。
        yAxis: [
          {
            // gridIndex: 0,
            // type: 'value',
            name: '点赞',
            splitLine: {
              show: false
            }
          },
          {
            // gridIndex: 0,
            // type: 'value',
            name: '收藏',
            splitLine: {
              show: false
            }
          },
          {
            gridIndex: 2,
            // type: 'value',
            name: '评论数',
            splitLine: {
              show: false
            }
          }
        ],
        // 声明多个 bar 系列，默认情况下，每个系列会自动对应到 dataset 的每一列。
        series: [
          {type: 'line', xAxisIndex: 0, yAxisIndex: 0, symbolSize: 5, connectNulls: true},
          {type: 'line', xAxisIndex: 1, yAxisIndex: 1, symbolSize: 5, connectNulls: true},
          {type: 'line', xAxisIndex: 2, yAxisIndex: 2, connectNulls: true}
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
  height: 700px;
  background: rgba(131, 153, 219, 0.4);
}
</style>