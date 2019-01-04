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
      </div>
    </el-col>
    <el-col :span="21">
      <div class='goods_right'>
        <router-view v-on:updata='getdata' v-bind:productid='goodsid' v-bind:vendorId='vendorId'>

        </router-view>
        <div class="footer">
          <p class="footer_p">版权所有©2017 深圳市云码互联数字技术有限公司 All Rights Reserved. 粤ICP备17040526号</p>
        </div>
      </div>
    </el-col>
  </el-row>
</div>
</template>
<style scoped>
.f-c:before, .f-c:after {
  content: "";
  display: table;
}
p:hover {
  text-decoration: none;
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
a:hover {
  text-decoration: none;
}
p:hover {
  text-decoration: none;
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
  import router from '../router.js'
  import common from '../common.js'

  export default{
    data(){
      return{
        childCon:'我是子页面',
        goodsid:'',
        vendorId:'',
        proNum:null,
        bar:[
        {
          name:'产品概况',
          path:'/goods/progaikuang',
          class:'el-icon-location-outline'
        },
        {
          name:'产品仓库 ',
          class:'el-icon-goods',
          childClass:'el-icon-goods',
          children:[
          {
            name:'产品管理',
            path:'/goods/pro_message'
          },
          {
            name:'产品分类',
            path:'/goods/classify'
          }
          ]
        },
        {
          name:'礼品仓库 ',
          class:'el-icon-star-on',
          childClass:'goods_sub3',
          children:[
          {
            name:'礼品管理',
            path:'/goods/gift'
          },
          {
            name:'分组管理',
            path:'/goods/groups'
          }
          ]
        },
        ]
      }
    },
    props:['datas'],
    methods:{
      init:function(){
        var self=this;
        self.vendorId=self.datas.vendorId;
      },
      showList:function(event){
        $(event.target).parents("li").find("ul").toggleClass("hidelist");
        $(event.target).parents("li").find('.arrow').toggleClass("upArrow");
      },
      getdata:function(id){
        this.goodsid=id;
      }
    },
    created:function(){
      this.init();
    }
  }
</script>
