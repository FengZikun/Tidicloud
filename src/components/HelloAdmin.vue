<template>
  <div class='fixed'>
    <div class="row logo">
      <div class="col-md-2">
        <div class="img-responsive">
          <router-link to="/admin/admingaikuang"><img src="../assets/img/5300dc4e4a1dd.jpg"></router-link>
        </div>
      </div>
      <div class="col-md-7 text-right">
        
      </div>
      <div class='username col-md-3'>
        <span class='span_one'></span>
        <ul class="personal">
          <li>
            admin
          </li>
          <a href="javascript:void(0)" @click='tuichu' style="text-decoration:none;"><li class="change_color">
            退出登录
          </li></a>
        </ul>
        
      </div>
      <div class='col-ma-2'></div>
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
  export default {
    name: 'hello',
    data () {
      return {
        msg: '',
        userName:null
      }
    },
    props:['vendorId'],
    methods:{
      init:function(){
        var self=this;
        self.userName=sessionStorage.getItem('userName');
      },
      tuichu:function(){
        var self=this;
        var url='http://cloud.tidicloud.com/cloud_code/POST/user/logout.do';
        var type='post';
        var data={
          userId:self.vendorId
        };
        var success=function(res){
          self.$emit('tuichu')
        };
        common.Ajax(url,type,data,success)
      }
    },
    created:function(){
      this.init()
    }
  }
</script>
