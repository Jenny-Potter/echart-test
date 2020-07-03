<template>
  <div class="container" @click="clickHandle('test click', $event)">

    <div class="userinfo" @click="bindViewTap">
      <img class="userinfo-avatar" v-if="userInfo.avatarUrl" :src="userInfo.avatarUrl" background-size="cover" />
      <div class="userinfo-nickname">
        <card :text="userInfo.nickName"></card>
      </div>
    </div>

    <van-tag>标签</van-tag>
    <van-tag type="danger">标签</van-tag>
    <van-tag type="primary">标签</van-tag>
    <van-tag type="success">标签</van-tag>

    <div class="usermotto">
      <div class="user-motto">
        <card :text="motto"></card>
      </div>
    </div>

    <form class="form-container">
      <input type="text" class="form-control" v-model="motto" placeholder="v-model" />
      <input type="text" class="form-control" v-model.lazy="motto" placeholder="v-model.lazy" />
    </form>
    <a href="/pages/counter" class="counter">去往Vuex示例页面</a>
    <div class="redbox" @click.stop="goToEchart"></div>
    <div class="greenbox" @click.stop="goToEchart1"></div>
    <div class="pinkbox" @click.stop="goToEchart2"></div>
    <div class="mask" v-if="open" @click.stop="open = false"></div>
    <div class="echarts-wrap" v-if="open">
    <mpvue-echarts :echarts="echarts" :onInit="initChart" canvasId="demo-canvas" />
    </div>
  </div>
</template>

<script>
import card from '@/components/card'
// import echarts from 'echarts'
import mpvueEcharts from 'mpvue-echarts'
import * as echarts from 'echarts/lib/echarts'
import 'echarts/lib/chart/line'
import 'echarts/lib/component/legend'
// import 'echarts/lib/component/tooltip'
// import 'echarts/lib/component/title'
// import 'echarts/lib/component/toolbox'
export default {
  mpType: 'page',
  components: {
    mpvueEcharts,
    card
  },
  data () {
    return {
      echarts,
      motto: 'Hello World',
      userInfo: {},
      dataTest: ['可爱', '美丽', '优雅'],
      dataTest1: ['可恶', '丑陋', '自卑'],
      legend: ['颜值'],
      legend1: ['恶心程度'],
      dataSelect: [],
      legendDataSelect: [],
      tag: '颜值',
      tag1: '恶心程度',
      tagSelect: '',
      open: false
    }
  },

  methods: {
    bindViewTap () {
      const url = '/packageA/logs'
      this.$router.push(url)
    },
    getUserInfo () {
      // 调用登录接口
      wx.login({
        success: () => {
          wx.getUserInfo({
            success: (res) => {
              this.userInfo = res.userInfo
            }
          })
        }
      })
    },
    clickHandle (msg, ev) {
      // eslint-disable-next-line
      this.open = false
      console.log('clickHandle:', msg, ev)
    },
    goToEchart () {
      this.$router.push({path: '/pages/echartTestAgain'})
      // this.open = true
      // this.dataSelect = this.dataTest
      // this.legendDataSelect = this.legend
      // this.tagSelect = this.tag
    },
    goToEchart2 () {
      this.$router.push({
        path: '/pages/dataSetTest'
      })
    },
    goToEchart1 () {
      // this.$router.push({path: '/pages/echartTestAgain'})
      this.open = true
      this.dataSelect = this.dataTest1
      this.legendDataSelect = this.legend1
      this.tagSelect = this.tag1
    },
    initChart (canvas, width, height) {
      let chart = echarts.init(canvas, null, {
        width: width,
        height: height
      })
      canvas.setChart(chart)
      chart.setOption(this.setOption(this.dataSelect, this.legendDataSelect, this.tagSelect))
      return chart
    },
    setOption (dataExample, legendData, tag) {
      let options = {
        xAxis: {
          data: dataExample
        },
        yAxis: {},
        legend: {
          data: legendData
        },
        series: [
          {
            name: tag,
            type: 'bar',
            data: [34, 67, 89]
          }
        ]

      }
      return options
    }

  },

  created () {
    // 调用应用实例的方法获取全局数据
    this.getUserInfo()
  }
}
</script>

<style scoped>
.userinfo {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.userinfo-avatar {
  width: 128rpx;
  height: 128rpx;
  margin: 20rpx;
  border-radius: 50%;
}

.userinfo-nickname {
  color: #aaa;
}


.form-control {
  display: block;
  padding: 0 12px;
  margin-bottom: 5px;
  border: 1px solid #ccc;
}

.counter {
  display: inline-block;
  margin: 10px auto;
  padding: 5px 10px;
  color: blue;
  border: 1px solid blue;
}
.redbox {
  width:30px;
  height:30px;
  background:red;
}
.greenbox {
  width:30px;
  height:30px;
  background:green;
}
.pinkbox {
  width:30px;
  height:30px;
  background:pink;
}
.mask {
  position:fixed;
  top:0;
  left:0;
  width:100%;
  height:100%;
  background:rgba(114, 111, 108,0.8);
  z-index:1020;
}
.echarts-wrap {
  width: 100%;
  height: 200px;
  z-index:1500;
  position:fixed;
  top:200px;
  left:0px;
  background:#fff
}
</style>
