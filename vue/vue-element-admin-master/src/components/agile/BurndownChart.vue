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
      default: '450px'
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
    setOptions({
      seriesName,
      xList,
      yList
    } = {}) {
      this.chart.setOption({
        backgroundColor: '#404A59',
        color: ['#ea9999', '#6fa8dc', '#8e7cc3', '#c27ba0', '#ffe599'],
        'title': [{
          'text': '手机银行迭代燃尽图',
          textStyle: {
            color: '#fff',
            fontWeight: 'bolder',
            fontSize: '25'
          },
          subtextStyle: {
            color: '#90979c',
            fontSize: '16'

          }
        },
        {
          text: '手机银行迭代燃尽占比',
          left: '83%',
          textStyle: {
            color: '#fff',
            fontWeight: 'bolder',
            fontSize: '25'
          }
        }
        ],
        'grid': {
          'borderWidth': 0,
          top: '20%',
          left: '2%',
          right: '25%',
          bottom: '5%',
          textStyle: {
            color: '#fff'
          }
        },
        'legend': {
          top: '8%',
          textStyle: {
            color: '#90979c'
          },
          'data': ['雄鹰组', '大象组', '猎豹组', '蜜罐组', '平均'],
          left: 'left'
        },
        'tooltip': {
          'trigger': 'axis',
          'axisPointer': {
            'type': 'shadow',
            textStyle: {
              color: '#fff'
            }

          }
        },

        'calculable': true,
        'xAxis': [{
          'type': 'category',
          'axisLine': {
            lineStyle: {
              color: '#90979c'
            }
          },
          'data': ['2020-05-18', '2020-05-19', '2020-05-20', '2020-05-21', '2020-05-22', '2020-05-25',
            '2020-05-26', '2020-05-27', '2020-05-28', '2020-05-29'
          ]
        }],
        'yAxis': [{
          top: '4%',
          'type': 'value',
          'splitLine': {
            'show': false
          },
          'axisLine': {
            lineStyle: {
              color: '#90979c'
            }
          }

        }],
        'series': [{
          'name': '雄鹰组',
          'type': 'bar',
          'stack': '总量',
          'barMaxWidth': 45,
          'barGap': '10%',
          'itemStyle': {
            'normal': {
              'label': {
                'show': true,
                'textStyle': {
                  'color': '#fff'
                },
                'position': 'inside',
                formatter: function(p) {
                  return p.value > 0 ? (p.value) : ''
                }
              }
            }
          },
          'data': [
            10,
            9,
            8,
            7,
            6,
            5
          ]
        },

        {
          'name': '大象组',
          'type': 'bar',
          'stack': '总量',
          'itemStyle': {
            'normal': {
              'barBorderRadius': 0,
              'label': {
                'show': true,
                'position': 'inside',
                formatter: function(p) {
                  return p.value > 0 ? (p.value) : ''
                }
              }
            }
          },
          'data': [
            10,
            9,
            8,
            7,
            6,
            5
          ]
        }, {
          'name': '猎豹组',
          'type': 'bar',
          'stack': '总量',
          'itemStyle': {
            'normal': {
              'barBorderRadius': 0,
              'label': {
                'show': true,
                'position': 'inside',
                formatter: function(p) {
                  return p.value > 0 ? (p.value) : ''
                }
              }
            }
          },
          'data': [
            10,
            9,
            8,
            7,
            6,
            5
          ]
        }, {
          'name': '蜜罐组',
          'type': 'bar',
          'stack': '总量',
          'itemStyle': {
            'normal': {
              'barBorderRadius': 0,
              'label': {
                'show': true,
                'position': 'inside',
                formatter: function(p) {
                  return p.value > 0 ? (p.value) : ''
                }
              }
            }
          },
          'data': [
            10,
            9,
            8,
            7,
            6,
            5
          ]
        }, {
          'name': '总数',
          'type': 'line',
          symbolSize: 10,
          symbol: 'circle',
          'itemStyle': {
            'normal': {
              'barBorderRadius': 0,
              'label': {
                'show': true,
                'position': 'top',

                formatter: function(p) {
                  return p.value > 0 ? (p.value) : ''
                }
              }
            }
          },
          'data': [
            40,
            36,
            32,
            28,
            24,
            20
          ]
        },
        {
          type: 'pie',
          center: ['90%', '53%'],
          radius: ['50%', '60%'],
          color: ['#ea9999', '#6fa8dc', '#8e7cc3', '#c27ba0', '#ffe599'],
          label: {
            normal: {
              position: 'center'
            }
          },
          data: [{
            value: 335,
            name: '直接访问'
          },
          {
            value: 310,
            name: '邮件营销'
          },
          {
            value: 234,
            name: '联盟广告'
          },
          {
            value: 135,
            name: '视频广告'
          },
          {
            value: 1548,
            name: '搜索引擎'
          }
          ]
        }
        ]
      })
    }
  }
}
</script>
