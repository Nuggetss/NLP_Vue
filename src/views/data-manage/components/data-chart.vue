<template>
  <div :class="className" :style="{height:height,width:width}" />
</template>

<script>
import echarts from 'echarts'
require('echarts/theme/macarons') // echarts theme

// const animationDuration = 6000

export default {
  name: 'DataChart',
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
    }
  },
  data() {
    return {
      chart: null,
      chartStyle: {
        dataNode: {
          color: '#1676A7',
          symbol: 'circle',
          symbolSize: [115, 65]
        }
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
      // 监听图标点击节点事件
      // var self = this
      this.chart.on('click', function(params) {
        if (params.componentType === 'series') {
          if (params.seriesType === 'graph') {
            if (params.dataType === 'node') {
              // 点击到了 graph 的 node（节点）上。
            }
          }
        }
      })
      this.chart.setOption({
        tooltip: {
          show: false
        },
        animationDurationUpdate: 1500,
        animationEasingUpdate: 'quinticInOut',
        hoverAnimation: true,
        textStyle: {
          fontSize: 14
        },
        series: [{
          name: '数据管理',
          type: 'graph',
          layout: 'none',
          label: {
            normal: {
              show: true
            }
          },
          edgeSymbol: ['circle', 'arrow'],
          edgeSymbolSize: [0, 0],
          lineStyle: {
            normal: {
              color: '#000000',
              opacity: 1,
              width: 1
            }
          },
          itemStyle: {
            normal: { color: this.chartStyle.dataNode.color }
          },
          symbol: this.chartStyle.dataNode.symbol,
          symbolSize: this.chartStyle.dataNode.symbolSize,
          data: [{
            name: '原始数据集',
            x: 0,
            y: 800
          }, {
            name: '中间过程数据集',
            x: 500,
            y: 600
          }, {
            name: '训练特征集',
            x: 1000,
            y: 400
          }, {
            name: '预处理模型对象',
            x: 1000,
            y: 800
          }, {
            name: '批处理特征集',
            x: 1500,
            y: 1000
          }, {
            name: '训练集',
            x: 1500,
            y: 220
          }, {
            name: '验证集',
            x: 1500,
            y: 400
          }, {
            name: '测试集',
            x: 1500,
            y: 580
          }, {
            name: '训练模型对象',
            x: 2000,
            y: 600
          }, {
            name: '结果对象',
            x: 2500,
            y: 1000
          }],
          links: [{
            source: 0,
            target: 1
          }, {
            source: 1,
            target: 2
          }, {
            source: 1,
            target: 3
          }, {
            source: 0,
            target: 4
          }, {
            source: 3,
            target: 4
          }, {
            source: 2,
            target: 5
          }, {
            source: 2,
            target: 6
          }, {
            source: 2,
            target: 7
          }, {
            source: 5,
            target: 8
          }, {
            source: 6,
            target: 8
          }, {
            source: 7,
            target: 8
          }, {
            source: 4,
            target: 9
          }, {
            source: 8,
            target: 9
          }]
        }]
      })
    }
  }
}
</script>
