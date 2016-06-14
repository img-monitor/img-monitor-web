<template>
  <div class="project">
    <sort-component></sort-component>
    <chart-component
      :current-type="currentType"
      :time-list="timeList"
      :current-type-name="currentTypeName"
      :current-time.sync="currentTime"
      :data="data"
    ></chart-component>

    <table-component
      :current-type.sync="currentType"
      :time-list="timeList"
      :current-type-name="currentTypeName"
      :current-time="currentTime"
      :data="data"
    ></table-component>
  </div>

</template>
<style>
  .project {
    background:#fff 0 -28px;

  }
</style>
<script>
  import Chart from '../chart/Chart.vue'
  import Table from '../chart/Table.vue'
  import Sort from '../chart/Sort.vue'
  export default{
    data: function() {
      return {
        timeList: [],
        currentType: 'successRatio',
        currentTypeName: '成功率',
        currentTime: 0,
        msg: 'project',
        data: {} //原始数据
      }
    },
    components:{
      'chart-component': Chart,
      'table-component': Table,
      'sort-component': Sort
    },
    created: function() { // 拉取数据
      var that = this;
      getData({}, function(json) {
        if (json && json.result == 0 && json.data) {
          let timeList = [];
          for (let i in json.data) {
            timeList.push(i);
          }

          if (timeList.length) {
            that.timeList = timeList;
            that.currentTime = timeList[timeList.length - 1];
            that.data = json.data;
          }

        } else {
          //todo .
        }
      });
    },
    watch: {
      'currentType': function(val, oldVal) {
        let name = {
          successRatio: '成功率',
          timeCost: '平均耗时',
          successLowFileRatio: '成功率不达标文件占比',
          timeCostHighFileRatio: '耗时不达标文件占比',
          http304CacheRatio: '304占比',
          localCacheRatio: '本地缓存占比',
          webpRatio: 'webp占比'
        }

        this.currentTypeName = name[val] || '';
      }
    },

    method: {

    }
  }



  //拉取数据
    var getData = function(params, callback) {
      var data = {};
      for (var i = 0; i < 7; i++) {
        data[Date.now() - i * 1000 * 60 * 60 * 24] = [
          {
            secondBusId: 1,
            secondBusName: '阅读',
            data: {
              successRatio: Math.random().toPrecision(2),
              timeCost: (Math.random() * 10).toPrecision(2),
              successLowFileRatio: Math.random().toPrecision(2),
              timeCostHighFileRatio:  Math.random().toPrecision(2),
              http304CacheRatio: Math.random().toPrecision(2),
              localCacheRatio: Math.random().toPrecision(2),
              webpRatio: Math.random().toPrecision(2)
            }
          },
          {
            secondBusId: 2,
            secondBusName: '动漫',
            data:  {
              successRatio: Math.random().toPrecision(2),
              timeCost: (Math.random() * 10).toPrecision(2),
              successLowFileRatio: Math.random().toPrecision(2),
              timeCostHighFileRatio:  Math.random().toPrecision(2),
              http304CacheRatio: Math.random().toPrecision(2),
              localCacheRatio: Math.random().toPrecision(2),
              webpRatio: Math.random().toPrecision(2)
            }
          }
        ]
      }
      callback({result: 0, data: data})
    }
</script>
