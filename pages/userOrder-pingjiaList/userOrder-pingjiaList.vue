<template>
	<view>
		<view class="mglr4">
			<view class="proRow">
				<view class="item" v-for="(item,index) in mainData.child" :key="index">
					<view class="fs12 flexRowBetween mgb10">
						<view class="color9">交易时间：{{item.create_time}}</view>
						<view class="red">已完成</view>
					</view>
					<view class="flexRowBetween">
						<view class="pic">
							<image :src="item.orderItem&&item.orderItem[0]&&item.orderItem[0].snap_product
							&&item.orderItem[0].snap_product.mainImg&&item.orderItem[0].snap_product.mainImg[0]?item.orderItem[0].snap_product.mainImg[0].url:''"
							 mode=""></image>
						</view>
						<view class="infor">
							<view class="avoidOverflow2 fs13">{{item.title}}</view>
							<view class="B-price flexRowBetween">
								<view class="price">{{item.unit_price}}</view>
								<view class="fs13">×{{item.count}}</view>
							</view>
						</view>
					</view>
					<view class="underBtn flexEnd mgt15" v-if="item.isremark==0">
						<view class="Bbtn" :data-id="item.id" @click="Router.navigateTo({route:{path:'/pages/userOrder-PingJia/userOrder-PingJia?id='+$event.currentTarget.dataset.id}})">去评价</view>
					</view>
					<view class="underBtn flexEnd mgt15" v-if="item.isremark==1">
						<view class="Bbtn">已评价</view>
					</view>
				</view>
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
				score:'',
				wx_info:{},
				mainData:[{},{},{}],
				mainData:{}
			}
		},
		
		onLoad(options) {
			const self = this;
			self.id = options.id;
			self.$Utils.loadAll(['getMainData'], self);
		},
		
		methods: {
			
			getMainData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					id: self.id,
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData = res.info.data[0];
					};
					console.log('self.mainData', self.mainData)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.orderGet(postData, callback);
			},
			
		}
	};
</script>

<style>
	@import "../../assets/style/orderNav.css";
	@import "../../assets/style/proList.css";
	@import "../../assets/style/editInfor.css";
	page{background: #F5F5F5;}
	
	.topNavFix{width: 100%;height: 220rpx;position: fixed;top: 0;right: 0;left: 0;box-sizing: border-box;z-index: 22;}
	.topNavH{height: 220rpx;}
	
	
	.tooling_indNav .list{height: 80rpx;}
	.tooling_indNav .list .item{line-height: 80rpx;}
	.navLisBox{white-space: nowrap;}
	.navLisBox .tt{display: inline-block;width: auto;margin:0 30rpx;}
	
	.proRow .item{margin-top: 30rpx;padding-top: 20rpx;}
	.proRow .item .pic{width: 160rpx;height: 160rpx;}
	.proRow .item .infor{width: 72%;height: 160rpx;}
	
	
	.adviseF5{padding: 20rpx 4%;background: #f5f5f5;border-radius: 10rpx;}
	.adviseF5 view{padding-bottom: 10rpx;}
	.adviseF5 view:last-child{padding-bottom: 0;}
	.hxEwm{width: 80rpx;height: 80rpx;}
	.hxEwm image{width: 100%;height: 100%;}
	
	.hxEwmShow{width: 70%;position: fixed;top: 45%;left: 50%;transform: translate(-50%,-50%);z-index: 50;}
	.hxEwmShow .ewm{width: 400rpx;height: 400rpx;display: block; margin: 0 auto;}
	.closeBtn{background: rgba(0,0,0,0.5);border: 0;top: auto;bottom: -130rpx;}
</style>
