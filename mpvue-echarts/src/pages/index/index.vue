<template>
  <div class="container">
    <a class="link"
      v-for="chart of charts"
      :key="chart.id"
      :href="chart.href">{{chart.name}}</a>
  </div>
</template>

<script>
import charts from './charts'

export default {
  computed: {
    charts() {
      return charts.map(chart => ({
        href: `/pages/demos/${chart.id}`,
        name: chart.name
      }))
    }
  }
}
</script>

<style scoped lang="less">
.link {
  width: 50%;
  text-align: center;
  padding: 10px 0;
}
</style>
