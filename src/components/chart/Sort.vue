<template>
   <div>
     <div class="rule">
       <p>
         <label>一级业务</label>
         <select>
           <option>特权中心</option>
           <option>特权中心特权中心</option>
           <option>Design</option>
           <option>IT</option>
         </select>
       </p>
     </div>

     <div class="rule">
       <p>
         <label>平台</label>
         <select>
           <option>android</option>
           <option>iOS</option>
           <option>全平台</option>
         </select>
       </p>
     </div>

     <div class="rule">
       <p>
         <label>时间区间</label>
         <input type="text" @click="showCalendar" v-model="value" placeholder="请输入日期">
         <calendar :show.sync="show" :value.sync="value" :x="x" :y="y" :begin="begin" :end="end" :range="range"></calendar>

       </p>
     </div>
     <div class="rule">
       <p>
         <button>查询</button>
       </p>
     </div>
   </div>
</template>
<style scoped>
   .rule {
     display: inline-block;
     margin: 10px;
   }

   .rule label{
     display: block;
     font-size: 17px;
     font-weight: bold;
   }
    select {
      border-color: #ddd;
      padding: 3px;
      border-radius: 5px;
      -webkit-appearance: menulist;
      align-items: center;
    }
</style>
<script>
  import Calendar from '../date/Calendar.vue'
    export default{
      data: function() {
        return {
          show:false,
          type:"date", //date datetime
          value:"2015-12-11",
          begin:"2015-12-20",
          end:"2015-12-25",
          x:0,
          y:0,
          range:true,//是否多选
        }
      },
      methods:{
        showCalendar:function(e){
          e.stopPropagation();
          var that=this;
          that.show=true;
          that.x=e.target.offsetLeft;
          that.y=e.target.offsetTop+e.target.offsetHeight+8;
          var bindHide=function(e){
            e.stopPropagation();
            that.show=false;
            document.removeEventListener('click',bindHide,false);
          };
          setTimeout(function(){
            document.addEventListener('click',bindHide,false);
          },500);
        }
      },
        components:{
          Calendar
        }
    }
</script>
