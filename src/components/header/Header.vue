<template>
  <div class="head">
    <div class="intro">
      <h1>图片监控系统</h1>
      <div>
        接口人:dreamzhu
        <a href="#">常见问题</a>
      </div>
    </div>

    <div class="user">
      <div>

        <span>{{rtx}}</span>
        <a v-if="rtx" href="#">退出</a></div>
    </div>
  </div>

</template>

<script>
  var Vue = require('vue');
  Vue.use(require('vue-resource'));


  module.exports =  {
    data () {
      return {
        rtx: ''
      }
    },
    created: function() {
      var that = this;
      getData({}, function(json) {
        if (json && json.result == 0 && json.data && json.data.rtx) {
          that.rtx = json.data.rtx;
        } else {
          //todo error
        }
      });
    },
  }

  function getData(params, callback) {
    Vue.http({url: '/index.html', method: 'GET'}).then(function (response) {
      callback({result: 0, data: {
        rtx: 'dreamzhu'
      }});
      // success callback
    }, function (response) {
      // error callback
    });

  }





</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

  .head {
    background:#313230;
    color: #fff;
    -moz-border-radius-topright:10px;
    border:0;
    margin:10px auto 0 auto;
    padding:5px 30px;
  }

  .intro {
    display: inline-block;
    width: 300px;
  }

  a {
    color:#888
  }


  a:hover {
    background:#383E3C
  }

  .user {
    display: inline-block;
    float:right;
  }

  .user span {
    padding:5px 5px;
  }
  /*h1 {*/
  /*color: #42b983;*/
  /*}*/
</style>
