<template>
  <div>
    <burndown-chart :chart-data="lineChartData" />
  </div>
</template>

<script>
import BurndownChart from '@/components/agile/BurndownChart.vue'
const lineChartData = {
  newVisitis: {
    expectedData: [100, 120, 161, 134, 105, 160, 165, 105, 160, 165],
    actualData: [120, 82, 91, 154, 162, 140, 145, 105, 160, 165],
    seriesName: '剩余故事数',
    yList: [100, 90, 80, 70, 60, 50, 40, 30, 15, 0],
    xList: ['2020-05-18', '2020-05-19', '2020-05-20', '2020-05-01', '2020-05-22', '2020-05-25', '2020-05-06', '2020-05-27', '2020-05-28', '2020-05-29']
  },
  messages: {
    expectedData: [200, 192, 120, 144, 160, 130, 140],
    actualData: [180, 160, 151, 106, 145, 150, 130]
  },
  purchases: {
    expectedData: [80, 100, 121, 104, 105, 90, 100],
    actualData: [120, 90, 100, 138, 142, 130, 130]
  },
  shoppings: {
    expectedData: [130, 140, 141, 142, 145, 150, 160],
    actualData: [120, 82, 91, 154, 162, 140, 130]
  }
}
export default {
  name: 'AgileDashboard',
  components: {
    BurndownChart
  },
  data() {
    return {
      lineChartData: lineChartData.newVisitis
    }
  }
}
</script>

<style>
</style>
