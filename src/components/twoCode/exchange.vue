<template>
	<div>
		<div class="mengban" v-show='showWarn'>
			<div class="warn">
				<div class="classifyHeader">
					<span style="display:block;height:48px;line-height:48px;font-weight: 600;">编辑备注</span>
				</div>
				<div class="warnmain">
					<span>填写备注：</span>
					<input class="message-value" type="text" name="" v-model='conmment'>
				</div>
				<div class="warnbottom">
					<input class="delbutton" type="button" name="" value="确定" @click='commit'>
					<input class="delbutton" type="button" name="" value="取消" @click='showWarn=false'>
				</div>
			</div>
		</div>
		<div class="top-title">
			<router-link to='/twoCode/signIn' class='title-two'>积分获取规则</router-link>
			<router-link to='/twoCode/IntegralUseRule' class='title-two'>积分使用规则</router-link>
			<router-link to='/twoCode/userInfomation' class='title-two'>用户信息</router-link>
			<router-link to='/twoCode/exchange' class='title-one'>兑换记录</router-link>
		</div>
		<div class="right-main">
			<div class="right-main-bottom">
				<p class="right-main-top1">
					<span class="right-main-top-icon1"></span>
					<span class="after">查看用户积分信息，可以输入关键字搜索</span>
				</p>
				<div class="button-group">
					<input class="message-value" placeholder="请输入用户名" type="text" name="">
					<input class="search-button" type="button" name="" value="搜索">
				</div>
				<div class="my-form">
					<ul class="pro-list">
						<li class="pro-li">
							<span class="pro-li-span">兑换ID</span>
							<span class="pro-li-span">订单ID</span>
							<span class="pro-li-span">微信昵称</span>
							<span class="pro-li-span">兑换礼品</span>
							<span class="pro-li-span">兑换时间</span>
							<span class="pro-li-span">操作</span>
						</li>
						<li class="pro-li" v-for='item in list'>
							<span class="pro-li-span">{{item.hisId}}</span>
							<span class="pro-li-span">{{item.orderId}}</span>
							<span class="pro-li-span"><img style="width: 65px;height: 65px;" :src="item.wxUserUrl">{{item.wxNickName}}</span>
							<span class="pro-li-span">{{item.exchangesName}}</span>
							<span class="pro-li-span">{{item.reveiceTime}}</span>
							<span class="pro-li-span">
								<span v-if='item.comment===""' class="beizhu" @click='showBeizhu(item.hisId)'></span>
								<span v-else @click='showBeizhu(item.hisId)'>{{item.comment}}</span>
							</span>
						</li>
					</ul>
				</div>
			</div>
			<div class="page-button">
				<div class="page-num">
					<ul class="page-num-ul">
						<a href="javascript:void(0)"><li class="page-num-li-arrow page-num-li" v-if='currentPage>1' @click='prevPage'><span class="arrow-left"></span></li></a>
						<a href="javascript:void(0)"><li class="page-num-li" v-if='currentPage>4&&totalPage.length!=1&&totalPage[0]!=1' v-bind:data-page='1' @click.self='changePage'>1</li></a>
						<a href="javascript:void(0)"><li class="page-num-li" v-if='currentPage>4&&totalPage.length!=1&&totalPage[0]!=1'>...</li></a>
						<a href="javascript:void(0)"><li class="page-num-li" v-for='item in totalPage' v-bind:class='{dangqianye:item==currentPage}' v-bind:data-page='item' @click.self='changePage'>{{item}}</li></a>
						<a href="javascript:void(0)"><li class="page-num-li" v-if='totalPages>5&&currentPage<totalPages-2'>...</li></a>
						<a href="javascript:void(0)"><li class="page-num-li" v-if='totalPages>5&&currentPage<totalPages-2' v-bind:data-page='resData.totalPages' @click.self='changePage'>{{resData.totalPages}}</li></a>

						<a href="javascript:void(0)"><li class="page-num-li page-num-li-arrow" v-if='currentPage<totalPages' @click='nextPage'><span class="arrow-right"></span></li></a>

					</ul>
				</div>
			</div>
		</div>
	</div>
</template>

<script type="text/javascript">
import common from '../../common.js'
import router from '../../router.js'
import {mapMutations} from 'vuex'
export default{
	data(){
		return{
			list:null,
				totalPage:[],    //页码数组
				currentPage:'',  //当前页
				totalPages:'',    //总页数
				showWarn:false,
				conmment:null,
				hisId:null
			}
		},
		props:['datas'],
		methods:{
			...mapMutations({
				checkDetail:'userDetail/checkDetail'
			}),
			init(currentPage){
				var self=this;
				var url='http://cloud.tidicloud.com/cloud_code/GET/vendorIntegral/getExchangeHistoryInfoList.do';
				var type='get';
				var data={
					vendorId:self.datas.vendorId,
					currentPage:currentPage,
					pageSize:10
				};
				var success=function(res){
					console.log(res)
					self.list=res.result.data;
					self.totalPages=res.totalPages;
					self.currentPage=res.currentPage;
					self.getPage();
				}
				common.Ajax(url,type,data,success)
			},
			//获取详情
			getDetail(id){
				this.checkDetail(id);
				router.push({path:'/twoCode/userDetail'})
			},

			//备注
			showBeizhu(id){
				this.showWarn=true;
				this.comment=null;
				this.hisId=id;
			},

			//备注
			commit(){
				var self=this;
				var url='http://cloud.tidicloud.com/cloud_code/POST/vendorIntegral/updateVendorIntegralPlayer.do';
				var type='post';
				var data={
					vendorId:self.datas.vendorId,
					hisId:self.hisId,
					conmment:self.conmment
				};
				var success=function(res){
					if(res.errorCode===0){
						self.showWarn=false;
						self.init(self.currentPage);
					}
				};
				common.Ajax(url,type,data,success)
			},
			//获取页数
			getPage:common.getPage,

			//翻页
			changePage:common.changePage,

			//上一页
			prevPage:common.prevPage,

			//下一页
			nextPage:common.nextPage,
		},
		mounted(){
			this.init();
		}
	}
	</script>

	<style scoped>
	.right-main-bottom{
		width: 95%;
		margin:auto;
		text-align: left;
	}
	.search-button{
		float: none;
	}
	.message-value{
		border: 1px solid #ccc;
		height: 30px;
		padding-left: 5px;
		border-radius: 5px;
	}
	.add-pro{
		margin-top: 40px;
	}
	.pro-li-span{
		width: 16%;
	}
	.right-main-top-icon1{
		width: 18px;
		height: 18px;
		background: url("../../assets/img/icon_tishi.png") no-repeat;
		float: left;
		margin-right: 8px;
	}
	.after{
		display: inline-block;
		color:#b3b3b7;
	}
	.right-main-top1{
		margin-top: 40px;
	}
	.search-button{
		width: 54px;
		height: 30px;
	}
	.warnbottom{
		text-align: center!important;;
		top: 132px;
		background: #f6f8fc;
		height: 40px;
		border-radius: 10px;
	}
	.delbutton{
		width: 89px;
		height: 34px;
		margin-top: 4px;
	}
	.warnbottom{
		left: 0;
	}
	</style>