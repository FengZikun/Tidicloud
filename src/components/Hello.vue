<template>
  <div class='fixed'>
    <div class="row logo">
      <div class="col-md-2">
        <div class="img-responsive">
          <router-link to="/enterprise">
            <img src="../assets/img/5300dc4e4a1dd.jpg">
          </router-link>
        </div>
      </div>
      <div class="col-md-7">
        <el-menu @select="menuSelect" :router="false" default-active="0" style="border-bottom-color: transparent;" class="el-menu-demo" mode="horizontal">
          <el-menu-item index="1" :route="{path: '/enterprise/shouyegaikuang'}">企业</el-menu-item>
          <el-menu-item index="2" :route="{path: '/goods/progaikuang'}">产品</el-menu-item>
          <el-menu-item index="3" :route="{path: '/twoCode/gaikuang' }">二维码</el-menu-item>
          <el-submenu index="4" style="line-height: 89px;">
            <template slot="title" style="line-height: 89px;">用户</template>
            <el-menu-item index="4-1">粉丝管理</el-menu-item>
            <el-menu-item index="4-2">会员管理</el-menu-item>
          </el-submenu>
          <el-menu-item index="5">公众号</el-menu-item>
          <el-menu-item index="6">商城</el-menu-item>
        </el-menu>
      </div>
      <div class='username col-md-3'>
        <span class='span_one'></span>
        <ul class="personal">
          <li>
            {{vendorName}}<span v-if='ceshi' style="color: #d5d7db;margin-left: 10px;">（试用用户）</span>
          </li>
          <li class="change_color">
            个人中心
          </li><li class="change_color">
            <a href="javascript:void(0)" @click='tuichu' style="text-decoration:none;">
              退出登录
            </a></li>
          </ul>
          
        </div>
      </div>

    </div>
  </template>

  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style lang="less">
 .fixed{
  a:hover{
    text-decoration: none;
  }
  .btn {
    border-radius: 0;
  }
  /*<!--logo和搜索框-->*/
  .img-responsive  img{
    width: 100px;
    float: left;
  }
  .img-responsive span {
    font-size: 18px;
    color: #00BAFF;
    padding-left: 12px;
    border-left: 1px solid #00BAFF;
  }
  .logo {
    width: 100%;
    height: 90px;
  }
  .logoR {
    position: absolute;
    left:210px;
    top:32px;
  }
  .logo .username {
    width: 23%;
    float: right;
    position: relative;
  }
  .logo .username .span_one {
    display: inline-block;
    width: 28px;
    height: 33px;
    background: url("../assets/img/icon_xinxi_2.png") no-repeat;
    float: left;
    background-position: center;
    height: 90px;
    line-height: 75px;
  }
  .logo .username .span_two {
    float: left;
    padding-left: 20px;
    font-size: 18px;
    padding-right: 20px;
    height: 60px;
    line-height: 60px;
  }
  .logo .username .span_three {
    display: inline-block;
    position: relative;
    left: -40px;
    width: 28px;
    height: 9px;
    background: url("../assets/img/icon_xia.png") no-repeat;
    /*float: left;*/
    margin-top: 41px;
    vertical-align: top;
  }
  .logo .username .span_four {
    display: inline-block;
    position: relative;
    left: -40px;
    width: 50px;
    height: 85px;
    background: url("../assets/img/icon_touxiang.png") no-repeat;
    /*float: left;*/
    background-position: center;
    background-size: contain;

  }
  .personal{
    display: inline-block;
    min-width: 130px;
    padding-left: 0;
    border-radius: 5px;
    overflow: hidden;
    position: absolute;
    left: 42px;
    top: 20px;
    z-index: 1;
    font-size: 18px;
    height: 50px;
    transition: 0.2s;
  }
  .personal:hover{
    height: 150px;
  }
  .change_color{
    background-color: #fff;
  }
  .change_color:hover{
    background: rgb(239, 243, 245)

  }
  #wqUser{
    width: 86px;
  }
  #wqUser:hover{
    height: 550px;
  }
  .xiajiantou{
    display: inline-block;
    width: 15px;
    height: 9px;
    background: url('../assets/img/icon_xia.png');
    background-repeat: no-repeat;
    position: relative;
    left: 7px;
  }
  .el-menu--horizontal>.el-menu-item{
    font-size: 16px;
    height: 89px;
    line-height: 89px;
  }
  .el-menu--horizontal>.el-submenu .el-submenu__title{
    height: 89px;
    line-height: 89px;
    font-size: 16px;

  }
 }
  
</style>
<script>
  import common from '../common.js'
  import router from '../router'
  import {mapState} from 'vuex'
  import {mapMutations} from 'vuex'

  export default {
    name: 'hello',
    data () {
      return {
        msg: '',
        vendorName:null,
        showWarn:false,
        warnText:'',
        ceshi:false
      }
    },
    props:['vendorId'],
    computed:{
      ...mapState({
        checkComment:state=>state.vendorId.checkComment
      })
    },
    methods:{
      ...mapMutations({
        getVendorId:'vendorId/getVendorId',
        getCheckComment:'vendorId/getCheckComment',
        logOut:'vendorId/logOut',
        show:'warn/show'
      }),
      menuSelect(index,path) {
        if(index === '1') {
          this.$router.push({
            path: "/enterprise/shouyegaikuang"
          })
        }
        if(index === '2') {
          this.$router.push({
            path: "/goods/progaikuang"
          })
        }
        if(index === '3') {
          this.$router.push({
            path: "/twoCode/gaikuang"
          })
        }
        if(index === '4-1') {
          // this.$router.push({
          //   path: "/enterprise/account"
          // })
          window.open('http://wq.tidicloud.com/web/index.php?c=mc&a=fans&', "blank")
          // window.open('http://wq.tidicloud.com', "blank")
        }
        if(index === '4-2') {
          // this.$router.push({
          //   path: "/enterprise/account"
          // })
          window.open('http://wq.tidicloud.com/web/index.php?c=mc&a=member&', "blank")
          // window.open('http://wq.tidicloud.com', "blank")

        }
        if(index === '5') {
          // this.$router.push({
          //   path: "/enterprise/account"
          // })
          window.open('http://wq.tidicloud.com', "blank")
          // window.open('http://wq.tidicloud.com', "blank")

        }
        if(index === '6') {
          // this.$router.push({
          //   path: "/enterprise/account"
          // })
          // window.open('http://wq.tidicloud.com', "blank")
          
          window.open('http://wq.tidicloud.com/web/index.php?c=site&a=entry&m=ewei_shopv2&do=web&r=shop', "blank")
        }
      },
      init:function(){
        var self=this;
        self.vendorName=sessionStorage.getItem('vendorName');
        if(self.checkComment!==undefined&&self.checkComment!==null){
          self.ceshi=true;
        }
      },
      tuichu:function(){
        var self=this;
        var url='http://cloud.tidicloud.com/cloud_code/POST/user/logout.do';
        var type='post';
        var data={
          userId:self.vendorId
        };

        var success=function(res){
          self.$emit('tuichu');
          self.getVendorId(null);
          self.getCheckComment(null);
          self.logOut();

        };
        common.Ajax(url,type,data,success)
      },
      changeColor:function(){
        var self=this;
        $(event.target).css('color','#00BAFF');
        $(event.target).parent().siblings().children().css('color','#6d7776')

      },
      toWeiQing:function(url){
        document.cookie=`_755url=${url.slice(url.indexOf('web/')+4)};domain=ym-a.top;path=/web`;
        let aa=window.open();
        setTimeout(function(){
          aa.location='http://mp.ym-a.top';
        }, 100);
      },
      toWeiQing1:function(url){
        document.cookie=`_755url=;domain=ym-a.top;path=/web`;
        let aa=window.open();
        setTimeout(function(){
          aa.location='http://mp.ym-a.top';
        }, 100);
      },
      WxGzhInfo:function(url,num){
        var self=this;
        $.ajax({
          url: 'http://cloud.tidicloud.com/cloud_code/GET/wxConfig/getWxGzhInfo.do',
          type:'get',
          data: {vendorId:self.vendorId},
          dataType: 'json',
          success: function (res) {
            if(res.status == "-1"){
              self.show('请先绑定公众号');
              router.push('/enterprise/en_public');
            }
            else{
              if(num==0){
                self.toWeiQing(url);
              }
              else if(num==1){
                self.toWeiQing(url);
              }
            }
          },
          error:function(res){
            //console.log(res);
          }
        });
      },
    },
    created:function(){
      this.init()
    }
  }
</script>
