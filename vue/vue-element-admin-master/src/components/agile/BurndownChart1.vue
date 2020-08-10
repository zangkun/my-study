<template>
  <div :class="className" :style="{height:height,width:width}" />
</template>

<script>
import echarts from 'echarts'
require('echarts/theme/macarons') // echarts theme
import resize from './mixins/resize'

export default {
  name: 'BurndownChart',
  mixins: [resize],
  props: {
    className: {
      type: String,
      default: 'chart'
    },
    width: {
      type: String,
      default: '100%'
    },
    height: {
      type: String,
      default: '350px'
    },
    autoResize: {
      type: Boolean,
      default: true
    },
    chartData: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      chart: null
    }
  },
  watch: {
    chartData: {
      deep: true,
      handler(val) {
        this.setOptions(val)
      }
    }
  },
  mounted() {
    this.$nextTick(() => {
      this.initChart()
    })
  },
  beforeDestroy() {
    if (!this.chart) {
      return
    }
    this.chart.dispose()
    this.chart = null
  },
  methods: {
    initChart() {
      this.chart = echarts.init(this.$el, 'macarons')
      this.setOptions(this.chartData)
    },
    foramt(xList, yList) {
      var yy = new Date().getFullYear()
      var mm = new Date().getMonth() + 1
      var dd = new Date().getDate()
      var xx
      var markPoints = new Array()
      for (var i = 0; i < yList.length; i++) {
        console.log(i)
        xx = xList[i].split('-')
        if ((yy == parseInt(xx[0])) && (mm == parseInt(xx[1])) && (dd == parseInt(xx[2]))) {
          markPoints.push({
            value: yList[i],
            xAxis: i,
            yAxis: yList[i]
          })
          return markPoints
        }
      }
      return markPoints
    },
    setOptions({
      seriesName,
      xList,
      yList
    } = {}) {
      this.chart.setOption({
        xAxis: {
          data: xList,
          boundaryGap: false,
          axisTick: {
            show: false
          }
        },
        grid: {
          left: 10,
          right: 10,
          bottom: 20,
          top: 30,
          containLabel: true
        },
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'cross'
          },
          padding: [5, 10]
        },
        yAxis: {
          axisTick: {
            show: false
          }
        },
        legend: {
          data: ['yList']
        },
        series: [{
          name: seriesName,
          itemStyle: {
            normal: {
              color: 'green',
              lineStyle: {
                color: 'green',
                width: 2
              }
            }
          },
          smooth: true,
          type: 'line',
          data: yList,
          markPoint: {
            symbol: 'pin', // 标记(气泡)的图形
            symbolSize: 50, // 标记(气泡)的大小
            itemStyle: {
              color: '#4587E7',
              borderColor: '#000',
              borderWidth: 0,
              borderType: 'solid'
            },
            data: this.foramt(xList, yList)
          }
        }]
      })
    }
  }
}
</script>
