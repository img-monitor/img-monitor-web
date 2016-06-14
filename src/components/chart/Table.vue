<template>
  <div class="content">
    <h3><span>{{  formatCurrentTime }}</span>详细数据</h3>
    <table v-if="currentTime">
      <thead>
      <tr>
        <th>项目</th>
        <th>成功率</th>
        <th>平均耗时</th>
        <th>成功率不达标文件占比</th>
        <th>耗时不达标文件占比</th>
        <th>304占比</th>
        <th>本地缓存占比</th>
        <th>webp占比</th>
      </tr>
      </thead>
      <tbody>
        <tr  v-for="item of dataList">
          <td >{{ item.secondBusName }}</td>
          <td v-on:click="changeType($event, 'successRatio')">{{ item.data.successRatio }}</td>
          <td v-on:click="changeType($event, 'timeCost')">{{ item.data.timeCost }}</td>
          <td v-on:click="changeType($event, 'successLowFileRatio')">{{ item.data.successLowFileRatio }}</td>
          <td v-on:click="changeType($event, 'timeCostHighFileRatio')">{{ item.data.timeCostHighFileRatio }}</td>
          <td v-on:click="changeType($event, 'http304CacheRatio')">{{ item.data.http304CacheRatio }}</td>
          <td v-on:click="changeType($event, 'localCacheRatio')">{{ item.data.localCacheRatio }}</td>
          <td v-on:click="changeType($event, 'webpRatio')">{{ item.data.webpRatio }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<style scoped>
  .content {
    margin:0 auto 0 auto;
    padding:0px 0px;
  }
  .content h3 {
    margin:0;
    padding: 0px 30px 10px 30px;
    background-color: #fff;
  }
  table {
    margin:0 auto 0 auto;
    width: 90%;
  }

  th {
    background: #434A48;
    color: #fff;
    padding: 7px 15px ;
    text-align: left;
    border: 1px solid #999;
  }

  td {
    background: #fff;
    padding: 7px 15px ;
    border: 1px solid #999;
  }

</style>
<script>
  var date = require('../../util/date.js');
  export default{
    props: ['timeList', 'currentType', 'currentTypeName', 'currentTime', 'data', 'msg'],
    computed: {
      dataList() {
        return this.data[this.currentTime] || [];
      },
      formatCurrentTime ( ) {
        return date.format("Y-m-d", this.currentTime);
      }
    },
    data(){
      return{
       // msg:'hello vue'
      }
    },
    ready() {

    },
    methods: {
      changeType: function(event, type) {
        this.currentType = type;
      }
    }
  }
</script>
