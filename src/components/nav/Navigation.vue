<template>
 <div>
   <ul class="navigation">
     <li><span class="active">按项目查询</span></li>
     <!--<li><a href="#">News</a></li>-->
     <!--<li><a href="#">Users</a></li>-->
   </ul>
 </div>
</template>

<script>
  export default {
    data () {
      return {
        // note: changing this line won't causes changes
        // with hot-reload because the reloaded component
        // preserves its current state and we are modifying
        // its initial state.
        msg: 'Hello World!!!!!'
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .navigation {
    background:#434A48;
    color:#fff;
    -moz-border-radius-bottomleft:10px;
    margin:0 auto 0px auto;
    padding:10px 30px;
  }

  .navigation > li {
    display:inline;
    color:#fff;

    margin:0
  }

  .navigation > li > a, .navigation > li > span {
    display:inline-block;
    padding:5px 10px;
    text-decoration:none;
  }

  .navigation a:hover {
    background:#383E3C
  }
  .navigation .active {
    background:#687370
  }



</style>
