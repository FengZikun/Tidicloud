<template>
  <div>
    <warn></warn>
    <el-row>
      <el-col :span="3">
        <div class='goods_left'>
          <el-menu
          :router="true"
          default-active="1"
          class="el-menu-vertical-demo"
          background-color="#313541"
          text-color="#fff"
          active-text-color="#ffd04b">
          <el-menu-item index="1" :route="{path: '/enterprise/shouyegaikuang'}">
            <i class="el-icon-location"></i>
            <span slot="title">系统概况</span>
          </el-menu-item>
          <el-submenu index="2">
            <template slot="title">
            <i class="el-icon-message"></i>
              <span>企业信息</span>
            </template>
            <el-menu-item index="2-1" :route="{path: '/enterprise/enterprise_message'}">
              基本信息
            </el-menu-item>
          </el-submenu>
          <el-submenu index="3">
            <template slot="title">
            <i class="el-icon-menu"></i>
              <span>账户管理</span>
            </template>
            <el-menu-item index="3-1" :route="{path: '/enterprise/revise'}">
              修改密码
            </el-menu-item>
            <el-menu-item index="3-2" :route="{path: '/enterprise/complete'}">
              完善资料
            </el-menu-item>
          </el-submenu>
        </el-menu>
        </div>
      </el-col>
      <el-col :span="21">
        <div class='goods_right'>
          <router-view v-on:upOrderId='getorderId' v-on:upvendorName='getvendorName' v-bind:datas='datas' v-bind:userId='userId' v-bind:vendorId='vendorId' v-bind:vendorName='vendorName' v-bind:orderId='orderId'></router-view>
          

          <div class="footer">
            <p class="footer_p">
              版权所有©2017 深圳市云码互联数字技术有限公司 All Rights Reserved. 粤ICP备17040526号
            </p>
          </div>
        </div>
      </el-col>
    </el-row>
  </div>
</template>
<style scoped>
.right-top,
.right-main,
.right-bottom{
  width: 95%;
  background: #fff;
  border-radius: 8px;
  margin: auto;
  margin-top: 44px;
  border-bottom: 1px solid transparent;
}
.gear{
  display: inline-block;
  width: 25px;
  height: 25px;
  vertical-align: middle;
  float: right;
  background: url(../../assets/img/icon_qiye_shezhi.png);
  background-size: cover;
}
.right-top p,
.right-main p,
.right-bottom p{
  font-family: "Microsoft YaHei";
}
.right-top-title{
  text-align: left;
  font-size: 18px;
  width: 95%;
  margin: auto;
  padding-top: 59px;
}
.right-main-li p{
  font-size: 17px;
  color: #6e787e;
}
.right-top-ul{
  width: 95%;
  margin:78px auto;
  padding-left: 0;
  display: flex;
  justify-content: space-between;
}
.right-main-ul{
  width: 85%;
  margin:78px auto;
  height: 170px;
  padding-left: 0;
  display: flex;
  justify-content: space-between;
}
.right-bottom-ul{
  width: 95%;
  list-style: square;
}
.right-bottom-li{
  text-align: left;
}
.right-top-li{
  float: left;
  width: 187px;
  height: 187px;
  border-radius: 8px;
  font-size: 22px;
  color: #fff;
  background-size: cover;
}
.right-top-li p:nth-of-type(1){
  height: 22px;
  line-height: 22px;
  margin: 41px 0 36px 0;
}
.right-top-li p:nth-of-type(2){
  font-size: 32px;
  height: 32px;
  line-height: 32px;
}
.right-top-li:nth-of-type(1){
  background: url(../../assets/img/png_1.png);
}
.right-top-li:nth-of-type(2){
  background: url(../../assets/img/png_2.png);
}
.right-top-li:nth-of-type(3){
  background: url(../../assets/img/png_3.png);
}
.right-top-li:nth-of-type(4){
  background: url(../../assets/img/png_4.png);
}
.right-top-li:nth-of-type(5){
  background: url(../../assets/img/png_5.png);
}
.right-top-li:nth-of-type(6){
  background: url(../../assets/img/png_6.png);
}
.pro-li:nth-of-type(1) .pro-li-span:nth-of-type(5):after{
  content: "";
  display: inline-block;
  width: 5px;
  height: 5px;
  background-color: #000;
}
.router-link-active{
  color: #fff!important;
  background-color: #00baff!important;
}
.el-menu-item{
  min-width: 100px;
}
.el-menu{
  text-align: left;
}

</style>
<script>
  import {mapState} from 'vuex'
  export default{
    data(){
      return{
        childCon:'我是子页面',
        checkall:true,
        vendorId:'',
        userId:'',
        vendorName:null,
        orderId:null,
        message:false,
        cer:false,
        public:false,
      }
    },
    props:['datas'],
    computed:{
      ...mapState({
        isTest:state=>state.vendorId.isTest
      })
    },
    methods:{
      init:function(){
        var self=this;
        self.vendorId=self.datas.vendorId;
        self.userId=self.datas.userId;
      },
      showList:function(event){
        $(event.target).parents("li").find("ul").toggleClass("hidelist");
        $(event.target).parents("li").find('.arrow').toggleClass("upArrow");
      },
      //获取用户名称
      getvendorName:function(data){
        var self=this;
        self.vendorName=data;
      },

      //获取订单id
      getorderId:function(id){
        var self=this;
        self.orderId=id;
      }
    },
    created:function(){
      this.init()
    }
  }
</script>
