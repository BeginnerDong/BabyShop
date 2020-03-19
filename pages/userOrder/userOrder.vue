<template>
	<view>
		
		<view class="topNavFix f5bj">
			<view class="tooling_indNav">
				<view class="list">
					<view class="item" :class="curr==1?'on':''" @click="changeCurr('1')">快递订单</view>
					<view class="item" :class="curr==2?'on':''" @click="changeCurr('2')">自提订单</view>
					<view class="item" :class="curr==3?'on':''" @click="changeCurr('3')">送货上门</view>
				</view>
			</view>
			
			<view class="orderNav whiteBj boxShaow color6 mgb15" v-show="curr==1">
				<scroll-view class="navLisBox fs13" scroll-x>
					<view class="tt" :class="serviceNum==1?'on':''" @click="serviceChange('1')">全部</view>
					<view class="tt" :class="serviceNum==2?'on':''" @click="serviceChange('2')">待付款</view>
					<view class="tt" :class="serviceNum==3?'on':''" @click="serviceChange('3')">待发货</view>
					<view class="tt" :class="serviceNum==4?'on':''" @click="serviceChange('4')">待收货</view>
					<view class="tt" :class="serviceNum==5?'on':''" @click="serviceChange('5')">已完成</view>
					<view class="tt" :class="serviceNum==6?'on':''" @click="serviceChange('6')">已评价</view>
					<view class="tt" :class="serviceNum==7?'on':''" @click="serviceChange('7')">退款/售后</view>
				</scroll-view>
			</view>
			
			<view class="orderNav whiteBj boxShaow color6 mgb15" v-show="curr==2">
				<scroll-view class="navLisBox fs13" scroll-x>
					<view class="tt" :class="selfTakeNum==1?'on':''" @click="selfTakeChange('1')">全部</view>
					<view class="tt" :class="selfTakeNum==2?'on':''" @click="selfTakeChange('2')">待付款</view>
					<view class="tt" :class="selfTakeNum==3?'on':''" @click="selfTakeChange('3')">待自提</view>
					<view class="tt" :class="selfTakeNum==4?'on':''" @click="selfTakeChange('4')">已自提</view>
					<view class="tt" :class="selfTakeNum==5?'on':''" @click="selfTakeChange('5')">已评价</view>
					<view class="tt" :class="selfTakeNum==6?'on':''" @click="selfTakeChange('6')">退款/售后</view>
				</scroll-view>
			</view>
			<view class="orderNav whiteBj boxShaow color6 mgb15"  v-show="curr==3">
				<scroll-view class="navLisBox fs13" scroll-x>
					<view class="tt" :class="deliveryNum==1?'on':''" @click="deliveryChange('1')">全部</view>
					<view class="tt" :class="deliveryNum==2?'on':''" @click="deliveryChange('2')">待付款</view>
					<view class="tt" :class="deliveryNum==3?'on':''" @click="deliveryChange('3')">待配送</view>
					<view class="tt" :class="deliveryNum==4?'on':''" @click="deliveryChange('4')">配送中</view>
					<view class="tt" :class="deliveryNum==5?'on':''" @click="deliveryChange('5')">已完成</view>
					<view class="tt" :class="deliveryNum==6?'on':''" @click="deliveryChange('6')">已评价</view>
					<view class="tt" :class="deliveryNum==7?'on':''" @click="deliveryChange('7')">退款/售后</view>
				</scroll-view>
			</view>
			
		</view>
		
		<view class="topNavH"></view>
		
		
		<view v-show="curr==1">
			<view class="mglr4">
				<view class="proRow">
					<view class="item">
						<view class="fs12 flexRowBetween mgb10">
							<view class="color9">交易时间：2020-01-18</view>
							<view class="red">待付款</view>
						</view>
						<view class="flexRowBetween">
							<view class="pic">
								<image src="../../static/images/the-orderl-img1.png" mode=""></image>
							</view>
							<view class="infor">
								<view class="avoidOverflow2 fs13">好孩子汤勺</view>
								<view class="B-price flexRowBetween">
									<view class="price">56.00</view>
									<view class="fs13">×1</view>
								</view>
							</view>
						</view>
						<view class="underBtn flexEnd mgt15">
							<view class="Bbtn red">去支付</view>
						</view>
					</view>
					<view class="item">
						<view class="fs12 flexRowBetween mgb10">
							<view class="color9">交易时间：2020-01-18</view>
							<view class="red">待发货</view>
						</view>
						<view class="flexRowBetween">
							<view class="pic">
								<image src="../../static/images/the-orderl-img1.png" mode=""></image>
							</view>
							<view class="infor">
								<view class="avoidOverflow2 fs13">好孩子汤勺</view>
								<view class="B-price flexRowBetween">
									<view class="price">56.00</view>
									<view class="fs13">×1</view>
								</view>
							</view>
						</view>
						<view class="underBtn flexEnd mgt15">
							<view class="Bbtn"  @click="Router.navigateTo({route:{path:'/pages/userOrder-PostSale/userOrder-PostSale'}})">退款/售后</view>
						</view>
					</view>
					<view class="item">
						<view class="fs12 flexRowBetween mgb10">
							<view class="color9">交易时间：2020-01-18</view>
							<view class="red">待收货</view>
						</view>
						<view class="flexRowBetween">
							<view class="pic">
								<image src="../../static/images/the-orderl-img1.png" mode=""></image>
							</view>
							<view class="infor">
								<view class="avoidOverflow2 fs13">好孩子汤勺</view>
								<view class="B-price flexRowBetween">
									<view class="price">56.00</view>
									<view class="fs13">×1</view>
								</view>
							</view>
						</view>
						<view class="underBtn flexEnd mgt15">
							<view class="Bbtn">确认收货</view>
						</view>
					</view>
					
					<view class="item">
						<view class="fs12 flexRowBetween mgb10">
							<view class="color9">交易时间：2020-01-18</view>
							<view class="red">已完成</view>
						</view>
						<view class="flexRowBetween">
							<view class="pic">
								<image src="../../static/images/the-orderl-img1.png" mode=""></image>
							</view>
							<view class="infor">
								<view class="avoidOverflow2 fs13">好孩子汤勺</view>
								<view class="B-price flexRowBetween">
									<view class="price">56.00</view>
									<view class="fs13">×1</view>
								</view>
							</view>
						</view>
						<view class="underBtn flexEnd mgt15">
							<view class="Bbtn" @click="Router.navigateTo({route:{path:'/pages/userOrder-PingJia/userOrder-PingJia'}})">去评价</view>
						</view>
					</view>
					<view class="item">
						<view class="fs12 flexRowBetween mgb10">
							<view class="color9">交易时间：2020-01-18</view>
							<view class="red">待发货</view>
						</view>
						<view class="flexRowBetween">
							<view class="pic">
								<image src="../../static/images/the-orderl-img1.png" mode=""></image>
							</view>
							<view class="infor">
								<view class="avoidOverflow2 fs13">好孩子汤勺</view>
								<view class="B-price flexRowBetween">
									<view class="price">56.00</view>
									<view class="fs13">×1</view>
								</view>
							</view>
						</view>
						<view class="borderB1 mgt15"></view>
						<view class="adviseF5 fs12 mgt15 color6">
							<view>挺好的，挺实用的非常好</view>
						</view>
					</view>
					<view class="item">
						<view class="fs12 flexRowBetween mgb10">
							<view class="color9">交易时间：2020-01-18</view>
							<view class="red">退款/售后</view>
						</view>
						<view class="flexRowBetween">
							<view class="pic">
								<image src="../../static/images/the-orderl-img1.png" mode=""></image>
							</view>
							<view class="infor">
								<view class="avoidOverflow2 fs13">好孩子汤勺</view>
								<view class="B-price flexRowBetween">
									<view class="price">56.00</view>
									<view class="fs13">×1</view>
								</view>
							</view>
						</view>
						<view class="borderB1 mgt15"></view>
						<view class="adviseF5 fs12 mgt15 color6">
							<view>退款原因：拍错了</view>
							<view>退款金额：￥138</view>
						</view>
					</view>		
				</view>
			</view>
		</view>
		
		<view v-show="curr==2">
			<view class="mglr4">
				<view class="proRow">
					<view class="item">
						<view class="fs12 flexRowBetween mgb10">
							<view class="color9">交易时间：2020-01-18</view>
							<view class="red">待付款</view>
						</view>
						<view class="flexRowBetween">
							<view class="pic">
								<image src="../../static/images/the-orderl-img1.png" mode=""></image>
							</view>
							<view class="infor">
								<view class="avoidOverflow2 fs13">好孩子汤勺</view>
								<view class="B-price flexRowBetween">
									<view class="price">56.00</view>
									<view class="fs13">×1</view>
								</view>
							</view>
						</view>
						<view class="underBtn flexEnd mgt15">
							<view class="Bbtn red">去支付</view>
						</view>
					</view>
					<view class="item">
						<view class="fs12 flexRowBetween mgb10">
							<view class="color9">交易时间：2020-01-18</view>
							<view class="red">待自提</view>
						</view>
						<view class="flexRowBetween">
							<view class="pic">
								<image src="../../static/images/the-orderl-img1.png" mode=""></image>
							</view>
							<view class="infor">
								<view class="avoidOverflow2 fs13">好孩子汤勺</view>
								<view class="B-price flexRowBetween">
									<view class="price">56.00</view>
									<view class="fs13">×1</view>
								</view>
							</view>
						</view>
						<view class="mgt15 flexRowBetween">
							<view class="">核销码：</view>
							<view class="hxEwm"  @click="hxEwmShow"><image src="../../static/images/the-orderl-img.png" mode=""></image></view>
						</view>
						<view class="underBtn flexEnd mgt15">
							<view class="Bbtn"  @click="Router.navigateTo({route:{path:'/pages/userOrder-PostSale/userOrder-PostSale'}})">退款/售后</view>
						</view>
					</view>
					
					<view class="item">
						<view class="fs12 flexRowBetween mgb10">
							<view class="color9">交易时间：2020-01-18</view>
							<view class="red">已自提</view>
						</view>
						<view class="flexRowBetween">
							<view class="pic">
								<image src="../../static/images/the-orderl-img1.png" mode=""></image>
							</view>
							<view class="infor">
								<view class="avoidOverflow2 fs13">好孩子汤勺</view>
								<view class="B-price flexRowBetween">
									<view class="price">56.00</view>
									<view class="fs13">×1</view>
								</view>
							</view>
						</view>
						<view class="underBtn flexEnd mgt15">
							<view class="Bbtn" @click="Router.navigateTo({route:{path:'/pages/userOrder-PingJia/userOrder-PingJia'}})">去评价</view>
						</view>
					</view>
					<view class="item">
						<view class="fs12 flexRowBetween mgb10">
							<view class="color9">交易时间：2020-01-18</view>
							<view class="red">待发货</view>
						</view>
						<view class="flexRowBetween">
							<view class="pic">
								<image src="../../static/images/the-orderl-img1.png" mode=""></image>
							</view>
							<view class="infor">
								<view class="avoidOverflow2 fs13">好孩子汤勺</view>
								<view class="B-price flexRowBetween">
									<view class="price">56.00</view>
									<view class="fs13">×1</view>
								</view>
							</view>
						</view>
						<view class="borderB1 mgt15"></view>
						<view class="adviseF5 fs12 mgt15 color6">
							<view>挺好的，挺实用的非常好</view>
						</view>
					</view>
					<view class="item">
						<view class="fs12 flexRowBetween mgb10">
							<view class="color9">交易时间：2020-01-18</view>
							<view class="red">退款/售后</view>
						</view>
						<view class="flexRowBetween">
							<view class="pic">
								<image src="../../static/images/the-orderl-img1.png" mode=""></image>
							</view>
							<view class="infor">
								<view class="avoidOverflow2 fs13">好孩子汤勺</view>
								<view class="B-price flexRowBetween">
									<view class="price">56.00</view>
									<view class="fs13">×1</view>
								</view>
							</view>
						</view>
						<view class="borderB1 mgt15"></view>
						<view class="adviseF5 fs12 mgt15 color6">
							<view>退款原因：拍错了</view>
							<view>退款金额：￥138</view>
						</view>
					</view>		
				</view>
			</view>
		</view>
		
		<view v-show="curr==3">
			<view class="mglr4">
				<view class="proRow">
					<view class="item">
						<view class="fs12 flexRowBetween mgb10">
							<view class="color9">交易时间：2020-01-18</view>
							<view class="red">待付款</view>
						</view>
						<view class="flexRowBetween">
							<view class="pic">
								<image src="../../static/images/the-orderl-img1.png" mode=""></image>
							</view>
							<view class="infor">
								<view class="avoidOverflow2 fs13">好孩子汤勺</view>
								<view class="B-price flexRowBetween">
									<view class="price">56.00</view>
									<view class="fs13">×1</view>
								</view>
							</view>
						</view>
						<view class="underBtn flexEnd mgt15">
							<view class="Bbtn red">去支付</view>
						</view>
					</view>
					<view class="item">
						<view class="fs12 flexRowBetween mgb10">
							<view class="color9">交易时间：2020-01-18</view>
							<view class="red">待配送</view>
						</view>
						<view class="flexRowBetween">
							<view class="pic">
								<image src="../../static/images/the-orderl-img1.png" mode=""></image>
							</view>
							<view class="infor">
								<view class="avoidOverflow2 fs13">好孩子汤勺</view>
								<view class="B-price flexRowBetween">
									<view class="price">56.00</view>
									<view class="fs13">×1</view>
								</view>
							</view>
						</view>
						<view class="underBtn flexEnd mgt15">
							<view class="Bbtn"  @click="Router.navigateTo({route:{path:'/pages/userOrder-PostSale/userOrder-PostSale'}})">退款/售后</view>
						</view>
					</view>
					<view class="item">
						<view class="fs12 flexRowBetween mgb10">
							<view class="color9">交易时间：2020-01-18</view>
							<view class="red">配送中</view>
						</view>
						<view class="flexRowBetween">
							<view class="pic">
								<image src="../../static/images/the-orderl-img1.png" mode=""></image>
							</view>
							<view class="infor">
								<view class="avoidOverflow2 fs13">好孩子汤勺</view>
								<view class="B-price flexRowBetween">
									<view class="price">56.00</view>
									<view class="fs13">×1</view>
								</view>
							</view>
						</view>
						<view class="underBtn flexEnd mgt15">
							<view class="Bbtn">确认收货</view>
						</view>
					</view>
					<view class="item">
						<view class="fs12 flexRowBetween mgb10">
							<view class="color9">交易时间：2020-01-18</view>
							<view class="red">已完成</view>
						</view>
						<view class="flexRowBetween">
							<view class="pic">
								<image src="../../static/images/the-orderl-img1.png" mode=""></image>
							</view>
							<view class="infor">
								<view class="avoidOverflow2 fs13">好孩子汤勺</view>
								<view class="B-price flexRowBetween">
									<view class="price">56.00</view>
									<view class="fs13">×1</view>
								</view>
							</view>
						</view>
						<view class="underBtn flexEnd mgt15">
							<view class="Bbtn" @click="Router.navigateTo({route:{path:'/pages/userOrder-PingJia/userOrder-PingJia'}})">去评价</view>
						</view>
					</view>
					<view class="item">
						<view class="fs12 flexRowBetween mgb10">
							<view class="color9">交易时间：2020-01-18</view>
							<view class="red">待发货</view>
						</view>
						<view class="flexRowBetween">
							<view class="pic">
								<image src="../../static/images/the-orderl-img1.png" mode=""></image>
							</view>
							<view class="infor">
								<view class="avoidOverflow2 fs13">好孩子汤勺</view>
								<view class="B-price flexRowBetween">
									<view class="price">56.00</view>
									<view class="fs13">×1</view>
								</view>
							</view>
						</view>
						<view class="borderB1 mgt15"></view>
						<view class="adviseF5 fs12 mgt15 color6">
							<view>挺好的，挺实用的非常好</view>
						</view>
					</view>
					<view class="item">
						<view class="fs12 flexRowBetween mgb10">
							<view class="color9">交易时间：2020-01-18</view>
							<view class="red">退款/售后</view>
						</view>
						<view class="flexRowBetween">
							<view class="pic">
								<image src="../../static/images/the-orderl-img1.png" mode=""></image>
							</view>
							<view class="infor">
								<view class="avoidOverflow2 fs13">好孩子汤勺</view>
								<view class="B-price flexRowBetween">
									<view class="price">56.00</view>
									<view class="fs13">×1</view>
								</view>
							</view>
						</view>
						<view class="borderB1 mgt15"></view>
						<view class="adviseF5 fs12 mgt15 color6">
							<view>退款原因：拍错了</view>
							<view>退款金额：￥138</view>
						</view>
					</view>		
				</view>
			</view>
		</view>
		
		<!-- 无数据 -->
		<view class="nodata"><image src="../../static/images/nodata.png" mode=""></image></view>
		
		<!-- 核销码放大弹框 -->
		<view class="black-bj" v-show="is_show"></view>
		<view class="hxEwmShow" v-show="is_hxEwmShow">
			<view><image class="ewm" src="../../static/images/the-orderl-img.png" mode=""></image></view>
			<view class="closeBtn" @click="hxEwmShow">×</view>
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
				is_show:false,
				curr:1,
				serviceNum:1,
				selfTakeNum:1,
				deliveryNum:1,
				is_hxEwmShow:false
			}
		},
		onLoad() {
			const self = this;
			//self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			changeCurr(curr){
				const self = this;
				if(curr!= self.curr){
					self.curr = curr
				}
			},
			serviceChange(serviceNum){
				const self = this;
				if(serviceNum!= self.serviceNum){
					self.serviceNum = serviceNum
				}
			},
			selfTakeChange(selfTakeNum){
				const self = this;
				if(selfTakeNum!= self.selfTakeNum){
					self.selfTakeNum = selfTakeNum
				}
			},
			deliveryChange(deliveryNum){
				const self = this;
				if(deliveryNum!= self.deliveryNum){
					self.deliveryNum = deliveryNum
				}
			},
			hxEwmShow(){
				const self = this;
				self.is_show = !self.is_show
				self.is_hxEwmShow = !self.is_hxEwmShow
			}
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
	
	.proRow .item{margin-bottom: 30rpx;padding-top: 20rpx;}
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
