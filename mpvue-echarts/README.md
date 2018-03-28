# 在微信小程序中使用 ECharts

> 本项目是 ECharts 的 Mpvue 小程序版本。开发者可以通过熟悉的 ECharts 配置方式及 Vue 语法，快速开发图表，满足各种可视化需求。

[![npm package](https://img.shields.io/npm/v/mpvue-echarts.svg)](https://npmjs.org/package/mpvue-echarts)
[![npm downloads](https://img.shields.io/npm/dm/mpvue-echarts.svg)](https://npmjs.org/package/mpvue-echarts)


## 安装

``` bash
npm i mpvue-echarts
```


## 使用
``` vue
<template>
  <div class="echarts-wrap">
    <mpvue-echarts :ec="ec" canvasId="demo-canvas" />
  </div>
</template>

<script>
import echarts from 'echarts'
import mpvueEcharts from 'mpvue-echarts'

let chart = null;

function initChart(canvas, width, height) {
  chart = echarts.init(canvas, null, {
    width: width,
    height: height
  });
  canvas.setChart(chart);

  var option = {}; // ECharts 配置项

  chart.setOption(option);

  // return chart; 不要返回 chart
}

export default {
  components: {
    mpvueEcharts
  },
  data () {
    return {
      ec: {
        onInit: initChart
      }
    }
  }
}
</script>

<style scoped>
.echarts-wrap {
  width: 100%;
  height: 300px;
}
</style>

```

这对于所有 ECharts 图表都是通用的，用户只需要修改上面 `option` 的内容，即可改变图表。`option` 的使用方法参见 [ECharts 配置项文档](http://echarts.baidu.com/option.html)。对于不熟悉 ECharts 的用户，可以参见 [5 分钟上手 ECharts](http://echarts.baidu.com/tutorial.html#5%20%E5%88%86%E9%92%9F%E4%B8%8A%E6%89%8B%20ECharts) 教程。

完整的例子请参见 [mpvue/examples](https://github.com/mpvue/examples/tree/master/mpvue-echarts) 项目。


## 属性

| 名称        | 类型           | 默认值         | 描述           |
| ------------|--------------- | ------------- | ------------- |
| ec          | Object         | {}            | echarts 配置  |
| canvasId    | String         | ec-canvas     | canvasId      |


## 常见问题

## FAQ

### 如何获取图表实例？

`echarts.init` 返回的即为图表实例。

### 如何延迟加载图表？

参见 `pages/lazyLoad` 的例子，可以在获取数据后再初始化数据。 

### 如何在一个页面中加载多个图表？

参见 `pages/multiCharts` 的例子。

### 为什么不支持 Tooltip？

因为 ECharts 中 tooltip 的实现是使用 HTML 渲染的，小程序不支持 DOM 操作，如果要支持的话，需要重新实现基于 Canvas 的 tooltip。这功能的工作量较大，不过用户反馈的需求也很大，所以接下来准备支持，需要等待一定时间。

### 打包时出错 `ERROR in static/js/vendor.js from UglifyJs`

参照以下配置使 babel 处理 mpvue-echarts
``` js
// webpack.base.conf.js
{
  test: /\.js$/,
  include: [
    resolve('src'),
    resolve('node_modules/mpvue-echarts')
  ],
  use: [
    'babel-loader',
    {
      loader: 'mpvue-loader',
      options: {
        checkMPEntry: true
      }
    }
  ]
}
```


## 微信版本要求

支持微信版本 >= 6.6.3，对应基础库版本 >= 1.9.91。

调试的时候，需要在微信开发者工具中，将“详情”下的“调试基础库”设为 1.9.91 及以上版本。

发布前，需要在 [https://mp.weixin.qq.com](https://mp.weixin.qq.com) 的“设置”页面，将“基础库最低版本设置”设为 1.9.91。当用户微信版本过低的时候，会提示用户更新。


## 暂不支持的功能

ECharts 中的绝大部分功能都支持小程序版本，因此这里仅说明不支持的功能，以及存在的问题。

以下功能尚不支持，如果有相关需求请在 [issue](https://github.com/ecomfe/echarts-for-weixin/issues) 中向我们反馈，对于反馈人数多的需求将优先支持：

- Tooltip
- 图片
- 多个 zlevel 分层

此外，目前还有一些 bug 尚未修复，部分需要小程序团队配合上线支持，但不影响基本的使用。已知的 bug 包括：

- 安卓平台：transform 的问题（会影响关系图边两端的标记位置、旭日图文字位置等）
- iOS 平台：半透明略有变深的问题
- iOS 平台：渐变色出现在定义区域之外的地方

如有其它问题，也欢迎在 [issue](https://github.com/ecomfe/echarts-for-weixin/issues) 中向我们反馈，谢谢！


## Todo

- [ ]  支持自定义 echarts 版本