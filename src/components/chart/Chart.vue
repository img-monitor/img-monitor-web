<template>
  <div  class="content"  >
    <div id="pageChart" style="height: 300px;"></div>
  </div>
</template>
<style scoped>
  .content {
    margin:0px auto 0 auto;
    padding:5px 30px;
    background: #fff;
  }
</style>
<script>

  var echarts = require('echarts');
  var date = require('../../util/date.js');

  var myChart;

  module.exports = {
    props: ['timeList', 'currentType', 'currentTypeName', 'currentTime', 'data'],
    data: function() {
      return {
      };
    },
    computed: {
      items() {//格式化数据
        let index = {};

        for(let time of this.timeList) {
          if (this.data[time]) {
            for (let bus of this.data[time]) {
              if (!index[bus.secondBusId]) {
                index[bus.secondBusId] = {
                  name: bus.secondBusName,
                  type: 'line',
                  data: []
                };
              }
              index[bus.secondBusId].data.push(bus.data[this.currentType]);
            }
          }
        }

        let items = [];
        for (let i in index) {
          items.push(index[i]);
        }

        return items;
      },
      formatTimeList() {
        var formatTimeList = [];
        for (let time of this.timeList) {
          formatTimeList.push(
            date.format("Y-m-d", time)
          );
        }

        return formatTimeList
      }
    },
    watch: {
      'currentType': function() {
        this.renderChart();
      }
    },
    ready: function() {
//      this.timeList = [1312,1]
      this.renderChart();
    },
    methods: {
      renderChart: function() {
        var that = this;
        if (!myChart) {
          myChart = echarts.init(document.getElementById('pageChart')); //初始化
          myChart.on('click', function (params) {
            that.currentTime = that.timeList[params.dataIndex]
          });
        }
        // 基于准备好的dom，初始化echarts实例
        // 绘制图表
        myChart.setOption({
          title: { text: that.currentTypeName || '图' },
          tooltip: {},
          xAxis: {
            data: that.formatTimeList
          },
          yAxis: {},
          series: that.items
        });
      }
    }
  }


</script>
