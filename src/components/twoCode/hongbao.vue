<template>
  <div>
    <div class="mengban" v-show='showWarn'>
      <div class="warn">
        <div class="classifyHeader">
          <span style="display:block;height:48px;line-height:48px;">下载红包记录</span>
        </div>
        <div class="warnmain">
          {{warnText}}
          <input type="month" name="" v-model='time'>
        </div>
        <div class="warnbottom">
          <input type="button" class="delbutton" name="" value="确定" @click='down'>
        </div>
      </div>
    </div>
    <div class='top-title'>
      <router-link to="/twoCode/hongbao" class='title-one'>红包</router-link>
      <router-link to="/twoCode/rule" class='title-two'>规则</router-link>
    </div>
    <div class="right-main">
      <div class="right-main-bottom">
        <div class="button-group">
          <router-link to='/twoCode/addHB'>
            <div class="add-pro">
              +&nbsp;添加红包
            </div>
          </router-link>
        </div>
        <div class="my-form">
          <ul class="pro-list">
            <li class="pro-li">
              <span class="pro-li-span head">订单ID</span>
              <span class="pro-li-span head">规则名称</span>
              <span class="pro-li-span head">充值金额</span>
              <span class="pro-li-span head">发放金额</span>
              <span class="pro-li-span head">有效时间</span>
              <span class="pro-li-span head">发放状态</span>
              <span class="pro-li-span head">查看详情</span>
            </li>
            <li class="pro-li" v-for='item in info'>
              <span class="pro-li-span">{{item.orderId}}</span>
              <span class="span2">{{item.ruleName}}</span>
              <span class="pro-li-span">{{item.consumeMoney}}</span>
              <span class="pro-li-span">{{item.rechargeMoney}}</span>
              <span class="pro-li-span" style="line-height:35px">{{item.startTime}}<br>{{item.endTime}}</span>
              <span class="pro-li-span"><span class="icon2"></span></span>
              <span class="pro-li-span"><img src="../../assets/img/icon_yulan.png" @click='showWarn=true'></span>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
  
</template>
<style scoped>
 /*@import "../assets/css/common.css";*/

.right-main-bottom{
  width: 95%;
  margin:auto;
  text-align: left;
}
.pro-li-span{
  width: 13%;
  height: 70px;
  line-height: 70px;
  vertical-align: middle;
}
.head{
  height: 60px;
  line-height: 60px;
}
.span2{
  display: inline-block;
  height: 70px;
  line-height: 70px;
  word-break: break-all;
  width: 13%;
  text-align: center;
  vertical-align: middle;
}
.button-group{
  margin-top: 40px;
}

.icon2{
  display: inline-block;
  width: 28px;
  height: 28px;
  background: url("../../assets/img/icon_dagou.png") no-repeat;
  line-height: 40px;
  text-align: center;
  vertical-align: middle;
}
.icon3{
  display: inline-block;
  width: 28px;
  height: 28px;
  background: url("../../assets/img/icon_cuowu.png") no-repeat;
  line-height: 40px;
  text-align: center;
  vertical-align: middle;
}
</style>
<!--<script src='../assets/js/china.js'></script>-->
<script>
  import '../../assets/js/echarts.js'
  import '../../assets/js/china.js'
  import common from '../../common.js'

  export default{
    data(){
      return{
        childCon:'我是子页面',
        currentPage:null,
        info:null,
        showWarn:false,
        warnText:'请选择下载日期',
        time:null
      }
    },
    props:['datas'],
    methods:{
      //初始化
      init:function(currentPage){
        var self=this;
        var url='http://cloud.tidicloud.com/cloud_code/GET/redEnv/info.do';
        var type='get';
        var data={
          pageSize:10,
          currentPage:currentPage,
          vendorId:parseInt(self.datas.vendorId)
        };
        var success=function(res){
          self.info=res.result.data;
        };
        common.Ajax(url,type,data,success);
      },

      //下载红包记录
      down(){
        var self=this;
        var url='http://cloud.tidicloud.com/cloud_code/redenvWallet/downloadWithdrawalsRecord.do?vendorId=' + parseInt(self.datas.vendorId) + '&time=' + self.time;
        window.location.href=url;
        self.showWarn=false;
      }
    },
    created:function(){
      this.init();
    }
  }
</script>
