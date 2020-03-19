<template>
	<view>
		<!-- 搜索 -->
		<view class="seachbox flexRowBetween whiteBj borderB1"  style="padding-bottom: 30rpx;"> 
			<view class="flex rr" style="width: 85%;">
				<button class="seachBtn" type="button">
					<image src="../../static/images/home-icon.png" mode=""></image>
				</button>
				<view class="input">
					<input type="text" name="" value="" placeholder="奶粉" placeholder-class="placeholder" />
				</view>
				<view class="delt flexCenter"><text>×</text></view>
			</view>
			<view class="fs15 pubColor" @click="Router.navigateTo({route:{path:'/pages/seachProduct/seachProduct'}})">搜索</view>
		</view>
		
		<view class="pdlr4 ">
			<view class="fs15 pdt20 pdb10 ftw">热门搜索</view>
			<view class="hotLabel flex center pdb10 borderB1">
				<view class="item" v-for="(item,index) in hotLabel" :key="index">{{item}}</view>
			</view>
			
			<view class="fs15 pdt15 pdb10 ftw">搜索记录</view>
			<view class="historyDate  center fs13 flex fs12">
				<view class="item" v-for="(item,index) in historyDate" :key="index">{{item}}</view>
			</view>
		</view>
		
		<view class="fx-deltBtn flexCenter color6" @click="popupShow">
			<image class="icon" src="../../static/images/addressl-icon3.png" mode=""></image>
			<text>清除搜索记录</text>
		</view>
		
		<view class="black-bj" v-show="is_show"></view>
		<view class="popupShow center whiteBj radius10 pdt20" v-show="is_popupShow">
			<view class="tip-title mgb10 fs15">提示</view>
			<view class="fs13 color6 pdb20 borderB1">确定清空搜索记录吗？</view>
			<view class="flex tip-button">
				<view class="item"  @click="popupShow">取消</view>
				<view class="item pubColor">确定</view>
			</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				showView: false,
				wx_info:{},
				is_show:false,
				hotLabel:['奶粉','餐具','玩具','纸尿裤','辅食','衣服'],
				historyDate:['奶粉','纸尿裤'],
				is_popupShow:false
			}
		},
		
		onLoad(options) {
			const self = this;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			popupShow(){
				const self=this;
				self.is_popupShow = !self.is_popupShow;
				self.is_show = !self.is_show;
				
			},
			getMainData() {
				const self = this;
				console.log('852369')
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				self.$apis.orderGet(postData, callback);
			}
		}
	};
</script>

<style>
	@import "../../assets/style/seach.css";
	
	page{padding-bottom: 110rpx;}
	
	
	.hotLabel{flex-wrap: wrap;}
	.hotLabel .item{width: 150rpx;height: 60rpx; line-height: 60rpx;background: #f0f0f0;margin:0 20rpx 20rpx 0; border-radius: 30rpx;text-align: center;}
	.hotLabel .item:nth-of-type(4n){margin-right: 0;}
	
	.historyDate .item{margin: 0 40rpx 30rpx 0;}
	.fx-deltBtn{width: 350rpx;height: 80rpx;line-height: 80rpx; border-radius: 40rpx;border:1px solid #a4a4a4; position: fixed;bottom: 70rpx;left: 50%;transform: translateX(-50%);}
	.fx-deltBtn .icon{width:36rpx; height: 36rpx;display: block;margin-right: 10rpx;}
	
	
	/* 删除弹框 */
	.popupShow{ width: 80%;position: fixed; top: 50%;left: 50%;transform: translate(-50%,-50%); z-index: 50;box-sizing: border-box;}
	.tip-button .item{width: 50%;box-sizing: border-box; line-height: 100rpx;}
	.tip-button .item:first-child{border-right:1px solid #eee;}
</style>

