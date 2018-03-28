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
  var item1 = {
    color: '#F54F4A'
  };
  var item2 = {
    color: '#FF8C75'
  };
  var item3 = {
    color: '#FFB499'
  };

  var data = [{
    children: [{
      value: 5,
      children: [{
        value: 1,
        itemStyle: item1
      }, {
        value: 2
      }, {
        value: 1
      }],
      itemStyle: item1
    }, {
      value: 10,
      children: [{
        value: 6,
        itemStyle: item3
      }, {
        value: 2,
        itemStyle: item3
      }, {
        value: 1
      }],
      itemStyle: item1
    }],
    itemStyle: item1
  }, {
    value: 9,
    children: [{
      value: 4,
      children: [{
        value: 2,
        itemStyle: item2
      }],
      itemStyle: item1
    }, {
      children: [{
        value: 3
      }],
      itemStyle: item3
    }],
    itemStyle: item2
  }, {
    value: 7,
    children: [{
      children: [{
        value: 1,
        itemStyle: item3
      }, {
        value: 3,
        itemStyle: item2
      }, {
        value: 2,
        itemStyle: item1
      }],
      itemStyle: item3
    }],
    itemStyle: item1
  }, {
    children: [{
      value: 6,
      children: [{
        value: 1,
        itemStyle: item2
      }, {
        value: 2,
        itemStyle: item1
      }, {
        value: 1,
        itemStyle: item3
      }],
      itemStyle: item3
    }, {
      value: 3,
      children: [{
        value: 1,
      }, {
        value: 1,
        itemStyle: item2
      }, {
        value: 1
      }],
      itemStyle: item3
    }],
    itemStyle: item1
  }];

  var option = {
    series: {
      radius: ['15%', '80%'],
      type: 'sunburst',
      sort: null,
      highlightPolicy: 'ancestor',
      data: data,
      label: {
        rotate: 'radial'
      },
      levels: [],
      itemStyle: {
        color: '#ddd',
        borderWidth: 2
      }
    },
    silent: true
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
