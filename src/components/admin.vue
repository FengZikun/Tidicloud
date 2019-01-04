<template>
  <div>
    <el-row>
      <el-col :span="3">
        <div class='goods_left'>
          <el-menu
          :router="true"
          default-active="0"
          class="el-menu-vertical-demo"
          style="margin-right: 0;"
          background-color="#313541"
          text-color="#fff"
          active-text-color="#ffd04b">
          <el-menu-item v-if="!item.children" v-for="(item, index) in bar" :index="index.toString()" :route="{path: item.path}">
            <i :class="item.class"></i>
            <span slot="title">{{item.name}}</span>
          </el-menu-item>
          <el-submenu v-else :index="index.toString()">
            <template slot="title">
              <i :class="item.class"></i>
              <span>{{item.name}}</span>
            </template>
            <el-menu-item v-for="(childItem, childIndex) in item.children" :index="index.toString() + '-' + childIndex.toString()" :route="{path: childItem.path}">{{childItem.name}}</el-menu-item>
          </el-submenu>
        </el-menu>
          <!-- <ul class='goods_menu'>
            <li class='goods_li goods_li_1' v-for='item in bar'>
              <router-link :to="item.path"><div class="change_color">
                <span class='img' :class='item.class'></span><a href="javascript:void(0)"><span>{{item.name}}</span></a>
              </div></router-link>
            </li>
          </ul> -->
        </div>
      </el-col>
      <el-col :span="21">
        <div class='goods_right'>
          <router-view @upId='getId' :userId='this.datas.userId' v-bind:detailId='this.detailId'>
            
          </router-view>
          <div class="footer">
            <p class="footer_p">版权所有©2017 深圳市云码互联数字技术有限公司 All Rights Reserved. 粤ICP备17040526号</p>
          </div>
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<script>
  export default{
    data(){
      return{
        childCon:'我是子页面',
        goodsid:'',
        detailId:null,
        bar:[
          {
            name:'概况',
            path:'/admin/admingaikuang',
            class:'el-icon-location-outline'
          },
          {
            name:'企业信息',
            path:'/admin/corporate',
            class:'el-icon-location-outline'
          },
          {
            name:'账号信息',
            path:'/admin/accountinfo',
            class:'el-icon-location-outline'
          },
          {
            name:'微信公众号信息',
            path:'/admin/weixin',
            class:'el-icon-location-outline'
          },
          {
            name:'企业账单',
            path:'/admin/enterpriseBill',
            class:'el-icon-location-outline'
          },
          {
            name:'待审核',
            path:'/admin/checkPending',
            class:'el-icon-location-outline'
          },
        ]
      }
    },
    props:['datas'],
    methods:{
      getdata:function(id){
        this.goodsid=id;
      },
      showList:function(event){
        $(event.target).parents("li").find("ul").toggleClass("hidelist");
        $(event.target).parents("li").find('.arrow').toggleClass("upArrow");
      },

      //监听ID
      getId:function(id){
        var self=this;
        self.detailId=id;
      }
    },
    created:function(){
      // this.init();
    }
  }
</script>

<style type="text/css">
  /*@import "../assets/css/common.css";*/
  .space3 {
    width: 100%;
    height: 100px;
  }
  .goods_menu .sub1 {
    width: 100%;
  }
  .goods_menu .sub1 li {
    line-height: 100%;
    margin-top: 10px;
  }
  .goods_menu .two_sub2 {
    width: 100%;
  }
  .goods_menu .two_sub2 li {
    line-height: 100%;
    margin-top: 10px;
  }
  .goods_menu .sub3 {
    width: 100%;
  }
  .goods_menu .sub3 li {
    line-height: 100%;
    margin-top: 10px;
  }
  .goods_menu .goods_li_2 .goods_sub2 {
    width: 100%;
    display: none;
  }
  .goods_menu .goods_li_3 .goods_sub3 {
    width: 100%;
    display: none;
  }
  .page-ckp-showNum {
    display: flex;
    justify-content: space-between;
    flex-direction: row;
    flex-wrap: nowrap;
    width: 100%;
    border-radius: 8px 8px 0 0;
    background-color: #f0f4fa;
    margin-top: 40px;
    margin-bottom: 40px;

  }
  .f-c:before, .f-c:after {
    content: "";
    display: table;
  }
  .page-ckp-showNum a {
    width: 30%;
    display: block;
    background-color: #fff;
    height: 365px;
    text-align: center;
    border-radius: 8px;
  }
  .page-ckp-showNum a:hover{
    box-shadow: 0 0 50px rgba(175,186,203,0.23);
  }
  .page-ckp-showNum .numIcon {
    height: 44px;
    padding-top: 60px;
  }
  .ui-chanpinku-num {
    display: inline-block;
    vertical-align: middle;
    background: url(../assets/img/chnpku.png) no-repeat;
    width: 92px;
    height: 99px;
  }
  .ui-chanpinku-num1 {
    background: url(../assets/img/icon_1.png) no-repeat;
  }
  .ui-chanpinku-num2 {
    background: url(../assets/img/icon_2.png) no-repeat;
  }
  .ui-chanpinku-num3 {
    background: url(../assets/img/icon_3.png) no-repeat;
  }
  .page-ckp-showNum .name {
    color: #000;
    padding-top: 161px;
    font-size: 21px;
  }
  .page-ckp-showNum .number {
    color: #333;
    padding-top: 3px;
    font-size: 32px;
  }
  p:hover {
    text-decoration: none;
  }
  .page-ckp-jinjie {
    width: 95%;
    height: 1055px;
    margin:0 auto;
    background-color: #fff;
    border-radius: 8px
  }
  .page-ckp-jinjie h3 {
    margin:0;
    padding-top: 60px;
    padding-left: 60px;
  }
  .f-l {
    display: inline;
    float: left;
  }
  .page-ckp-jinjie h3 .f-l {
    line-height: 30px;
    color: #333;
    font-size: 16px;
    font-weight: 400;
  }
  .btBig, .btBig:visited, .btBig:hover {
    background: #44bb44;
    color: #fff;
    display: inline-block;
    font-size: 14px;
    text-align: center;
    cursor: pointer;
    height: 30px;
    line-height: 30px;
    padding: 0 24px;
    border: 0;
    border-radius: 3px;
    /*padding-left: 42px;*/
  }
  .btBig:before {
    /*border-left: 2px solid #fff;
    left: 29px;
    top: 9px;*/
    position: absolute;
    width: 12px;
    height: 12px;
    content: "";
  }
  .page-ckp-jinjie ul {
    width: 100%;
    margin: 0;
    padding: 0;
  }
  .page-ckp-jinjie ul li {
    width: 100%;
    height: 200px;
    float: left;
    transition: all .3s ease;
    margin-bottom: 10px;
    box-sizing: border-box;
    /*padding-right: 20px;*/
    margin-top: 20px;
  }
  .page-ckp-jinjie ul li .left-icon {
    display: inline-block;
    vertical-align: middle;
    width: 20%;
    height: 119px;
    float: left;
    vertical-align: middle;
    text-align: center;
  }
  .flower{
    display: block;
    width: 119px;
    height: 119px;
    margin: auto;
    background: url(../assets/img/icon_hua.png) no-repeat;
  }
  .right-text{
    display: inline-block;
    width: 80%;
  }
  .intro{
    display: block;
    color: #000;
    text-align: left;
    font-family: 'Microsoft YaHei';
  }
  .page-ckp-jinjie ul li .circle {
    width: 80px;
    height: 80px;
    border-radius: 100%;
    background-color: #f4f5f9;
    display: block;
    margin: 26px auto 0;
    position: relative;
  }
  .page-ckp-jinjie ul li .circle .ui-chanpinku-jinjie {
    position: absolute;
    left: 0;
    top: 0;
    bottom: 0;
    right: 0;
    margin: auto;
  }
  .page-ckp-jinjie ul li p {
    font-size: 14px;
    color: #888;
    line-height: 143%;
    padding-top: 12px;
    text-align: left;
  }
  a:hover {
    text-decoration: none;
  }
  p:hover {
    text-decoration: none;
  }
  
</style>

