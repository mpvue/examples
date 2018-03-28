<template>
  <div class="container">
    <div class="wrap">
      <mpvue-echarts :ec="ec" />
    </div>
  </div>
</template>

<script>
import echarts from 'echarts'
import mpvueEcharts from 'mpvue-echarts'

function initChart(canvas, width, height) {
  const chart = echarts.init(canvas, null, {
    width: width,
    height: height
  });
  canvas.setChart(chart);

  var option = {
    color: ['#37a2da'],
    parallelAxis: [
      { dim: 0, name: 'Price' },
      { dim: 1, name: 'Net Weight' },
      { dim: 2, name: 'Amount' },
      {
        dim: 3,
        name: 'Score',
        type: 'category',
        data: ['Excellent', 'Good', 'OK', 'Bad']
      }
    ],
    parallel: {
      left: 40,
      right: 80,
      top: 50,
      bottom: 20,
      parallelAxisDefault: {
        axisLine: {
          lineStyle: {
            color: '#999'
          }
        },
        axisLabel: {
          color: '#666'
        },
        nameTextStyle: {
          color: '#666'
        }
      }
    },
    series: {
      type: 'parallel',
      lineStyle: {
        width: 4
      },
      data: [
        [12.99, 100, 82, 'Good'],
        [9.99, 80, 77, 'OK'],
        [20, 120, 60, 'Excellent'],
        [3.2, 40, 70, 'OK']
      ]
    }
  };

  chart.setOption(option);
  return chart;
}

export default {
  data () {
    return {
      ec: {
        onInit: initChart
      }
    }
  },

  components: {
    mpvueEcharts
  },
}
</script>

<style scoped lang="less">
.wrap {
  width: 100%;
  height: 300px;
}
</style>
