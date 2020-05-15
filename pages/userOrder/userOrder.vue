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
					<view class="tt" :class="status==1?'on':''" @click="changeStatus('1')">全部</view>
					<view class="tt" :class="status==2?'on':''" @click="changeStatus('2')">待付款</view>
					<view class="tt" :class="status==3?'on':''" @click="changeStatus('3')">待发货</view>
					<view class="tt" :class="status==4?'on':''" @click="changeStatus('4')">待收货</view>
					<view class="tt" :class="status==5?'on':''" @click="changeStatus('5')">已完成</view>
					<view class="tt" :class="status==6?'on':''" @click="changeStatus('6')">已评价</view>
					<view class="tt" :class="status==7?'on':''" @click="changeStatus('7')">退款/售后</view>
				</scroll-view>
			</view>
			
			<view class="orderNav whiteBj boxShaow color6 mgb15" v-show="curr==2">
				<scroll-view class="navLisBox fs13" scroll-x>
					<view class="tt" :class="statusTwo==1?'on':''" @click="changeStatusTwo('1')">全部</view>
					<view class="tt" :class="statusTwo==2?'on':''" @click="changeStatusTwo('2')">待付款</view>
					<view class="tt" :class="statusTwo==3?'on':''" @click="changeStatusTwo('3')">待自提</view>
					<view class="tt" :class="statusTwo==4?'on':''" @click="changeStatusTwo('4')">已自提</view>
					<view class="tt" :class="statusTwo==5?'on':''" @click="changeStatusTwo('5')">已评价</view>
					<view class="tt" :class="statusTwo==6?'on':''" @click="changeStatusTwo('6')">退款/售后</view>
				</scroll-view>
			</view>
			<view class="orderNav whiteBj boxShaow color6 mgb15"  v-show="curr==3">
				<scroll-view class="navLisBox fs13" scroll-x>
					<view class="tt" :class="status==1?'on':''" @click="changeStatus('1')">全部</view>
					<view class="tt" :class="status==2?'on':''" @click="changeStatus('2')">待付款</view>
					<view class="tt" :class="status==3?'on':''" @click="changeStatus('3')">待配送</view>
					<view class="tt" :class="status==4?'on':''" @click="changeStatus('4')">配送中</view>
					<view class="tt" :class="status==5?'on':''" @click="changeStatus('5')">已完成</view>
					<view class="tt" :class="status==6?'on':''" @click="changeStatus('6')">已评价</view>
					<view class="tt" :class="status==7?'on':''" @click="changeStatus('7')">退款/售后</view>
				</scroll-view>
			</view>
			
		</view>
		
		<view class="topNavH"></view>
		
		
		<view>
			<view class="mglr4">
				<view class="proRow">
					<view class="item" v-for="(item,index) in mainData" :key="index">
						<view class="fs12 flexRowBetween mgb10">
							<view class="color9">交易时间：{{item.create_time}}</view>
							<view class="red" v-if="item.pay_status==0">待付款</view>
							<view class="red" v-if="item.pay_status==1&&item.transport_status==0&&item.transport_type==2&&item.order_step==0">待发货</view>
							<view class="red" v-if="item.pay_status==1&&item.transport_status==1&&item.transport_type==2&&item.order_step==0">待收货</view>
							<view class="red" v-if="item.pay_status==1&&item.transport_status==2&&item.transport_type!=1&&item.order_step==0">已完成</view>
							<view class="red" v-if="item.pay_status==1&&item.order_step>0">退款/售后</view>
							<view class="red" v-if="item.pay_status==1&&(item.transport_status==0||item.transport_status==1)&&item.transport_type==1&&item.order_step==0">待自提</view>
							<view class="red" v-if="item.pay_status==1&&item.transport_status==2&&item.transport_type==1&&item.order_step==0">已自提</view>
							<view class="red" v-if="item.pay_status==1&&item.transport_status==0&&item.transport_type==3&&item.order_step==0">待配送</view>
							<view class="red" v-if="item.pay_status==1&&item.transport_status==1&&item.transport_type==3&&item.order_step==0">配送中</view>
						</view>
						<view  v-for="(c_item,c_index) in item.child">
							<view class="flexRowBetween">
								<view class="pic">
									<image :src="c_item.orderItem&&c_item.orderItem[0]&&c_item.orderItem[0].snap_product&&c_item.orderItem[0].snap_product.product&&
								c_item.orderItem[0].snap_product.product.mainImg&&c_item.orderItem[0].snap_product.product.mainImg[0]?c_item.orderItem[0].snap_product.product.mainImg[0].url:''" mode=""></image>
								</view>
								<view class="infor">
									<view class="avoidOverflow2 fs13">{{c_item.orderItem&&c_item.orderItem[0]&&c_item.orderItem[0].snap_product
								&&c_item.orderItem[0].snap_product&&c_item.orderItem[0].snap_product.product?c_item.orderItem[0].snap_product.product.title:''}}</view>
								<view class="d-flex fs12 color6">
									<view class="specsBtn mr-1">{{c_item.orderItem&&c_item.orderItem[0]&&c_item.orderItem[0].snap_product
								&&c_item.orderItem[0].snap_product?c_item.orderItem[0].snap_product.title:''}}</view>
								</view>
									<view class="B-price flexRowBetween">
										<view class="price">{{c_item.unit_price?c_item.unit_price:''}}</view>
										<view class="fs13">×{{c_item.count?c_item.count:''}}</view>
									</view>
								</view>
							</view>
							<view class="borderB1 mgt15" v-if="c_item.isremark==1"></view>
							<view class="adviseF5 fs12 mgt15 color6" v-if="c_item.isremark==1">
								<view>{{c_item.remark&&c_item.remark[0]?c_item.remark[0].description:''}}</view>
							</view>
						</view>
						<view class="mgt15 flexRowBetween"  v-if="item.order_step==0&&item.pay_status==1&&item.transport_status==0&&item.transport_type==1">
							<view class="">核销码：</view>
							<view class="hxEwm"  @click="hxEwmShow(index)"><image :src="item.qrcode" mode=""></image></view>
						</view>
						<view class="underBtn flexEnd mgt15" v-if="item.pay_status==0">
							<view class="Bbtn red" @click="goPay(index)">去支付</view>
						</view>
						<view class="underBtn flexEnd mgt15" v-if="((item.pay_status==1&&item.transport_status==0&&item.group_status==0)||(item.pay_status==1&&item.group_status==1))&&item.order_step==0">
							<view class="Bbtn" :data-id="item.id"  @click="Router.navigateTo({route:{path:'/pages/userOrder-PostSale/userOrder-PostSale?id='+$event.currentTarget.dataset.id}})">退款/售后</view>
						</view>
						<view class="underBtn flexEnd mgt15" v-if="item.pay_status==1&&item.transport_status==1">
							<view class="Bbtn" @click="orderUpdate(index)">确认收货</view>
						</view>
						<view class="underBtn flexEnd mgt15" v-if="item.pay_status==1&&item.group_status==1">
							<view class="Bbtn">未成团</view>
						</view>
						<view class="underBtn flexEnd mgt15" v-if="item.pay_status==1&&item.group_status==2">
							<view class="Bbtn">已成团</view>
						</view>
						<view class="underBtn flexEnd mgt15" v-if="item.pay_status==1&&item.transport_status==2&&item.isremark==0">
							<view class="Bbtn" :data-id="item.id" @click="Router.navigateTo({route:{path:'/pages/userOrder-pingjiaList/userOrder-pingjiaList?id='+$event.currentTarget.dataset.id}})">去评价</view>
						</view>
						<view v-if="order_step==1&&item.pay_status==1&&item.transport_status==2">
							<view class="borderB1 mgt15"></view>
							<view class="adviseF5 fs12 mgt15 color6">
								<view>退款原因：{{item.explain?item.explain:''}}</view>
								<view>退款金额：￥{{item.price}}</view>
							</view>
						</view>
						
					</view>	
				</view>
			</view>
		</view>
		 
		
		
		<!-- 无数据 -->
		<view class="nodata"  v-if="mainData.length==0"><image src="../../static/images/nodata.png" mode=""></image></view>
		
		<!-- 核销码放大弹框 -->
		<view class="black-bj" v-show="is_show"></view>
		<view class="hxEwmShow" v-show="is_hxEwmShow">
			<view><image class="ewm" :src="mainData[chooseIndex].qrcode" mode=""></image></view>
			<view class="closeBtn" @click="hxEwmShow">×</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
			  	
				curr:1,
				status:1,
				statusTwo:1,
				
				is_hxEwmShow:false,
				searchItem:{
					level:1,
					transport_type:2
				},
				mainData:[],
				chooseIndex:-1
			}
		},
		
		onLoad(options) {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			//self.$Utils.loadAll(['getMainData'], self);
		},
		
		onShow() {
			const self = this;
			self.getMainData(true)
		},
		
		methods: {
			
			orderUpdate(index) {
				const self = this;
				uni.setStorageSync('canClick', false);
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.data = {
					transport_status:2,
				};
				postData.searchItem = {
					id:self.mainData[index].id,
				};
				const callback = (data) => {
					uni.setStorageSync('canClick', true);
					if (data && data.solely_code == 100000) {
						self.$Utils.showToast('操作成功','none');
						setTimeout(function() {
							self.getMainData(true)
						}, 1000);
					} else {
						self.$Utils.showToast(data.msg,'none')
					}
				};
				self.$apis.orderUpdate(postData, callback);
			 },
			
			goPay(index) {
				const self = this;	
				uni.setStorageSync('canClick',false);
				const postData = {
					wxPay:{
						price: parseFloat(self.mainData[index].price)
					}
				}
				postData.tokenFuncName = 'getProjectToken',
				postData.searchItem = {
					id: self.mainData[index].id
				};	
				const callback = (res) => {
					if (res.solely_code == 100000) {
						uni.setStorageSync('canClick', true);
						if (res.info) {
							const payCallback = (payData) => {
								console.log('payData', payData)
								if (payData == 1) {
									uni.showToast({
										title: '支付成功',
										duration: 1000,
										success: function() {
											
										}
									});
									setTimeout(function() {
										self.getMainData(true)
									}, 1000);
								} else {
									uni.setStorageSync('canClick', true);
								};
							};
							self.$Utils.realPay(res.info, payCallback);
						} else {
							
							uni.showToast({
								title: '支付成功',
								duration: 1000,
								success: function() {
									
								}
							});
							setTimeout(function() {
								self.getMainData(true)
							}, 1000);
						};
					} else {
						uni.setStorageSync('canClick', true);
						uni.showToast({
							title: '调起支付失败',
							duration: 2000
						});
					};
				};
				self.$apis.pay(postData, callback);
			},
			
			changeCurr(curr){
				const self = this;
				if(curr!= self.curr){
					self.curr = curr;
					delete self.searchItem.transport_status;
					delete self.searchItem.pay_status;
					delete self.searchItem.order_step;
					delete self.searchItem.isremark;
					self.status = 1;
					if(self.curr==1){
						self.searchItem.transport_type = 2
					}else if(self.curr==2){
						self.searchItem.transport_type = 1
					}else if(self.curr==3){
						self.searchItem.transport_type = 3
					};
					self.getMainData(true)
				}
			},
			
			changeStatus(status){
				const self = this;
				if(status!= self.status){
					self.status = status;
					if(self.status==1){
						delete self.searchItem.transport_status;
						delete self.searchItem.pay_status;
						delete self.searchItem.order_step;
						delete self.searchItem.isremark;
					}else if(self.status==2){
						self.searchItem.pay_status=0
					}else if(self.status==3){
						self.searchItem.pay_status=1;
						self.searchItem.transport_status=0;
						self.searchItem.isremark=0
						self.searchItem.order_step=0
					}else if(self.status==4){
						self.searchItem.pay_status=1;
						self.searchItem.transport_status=1;
						self.searchItem.isremark=0
						self.searchItem.order_step=0
					}else if(self.status==5){
						self.searchItem.pay_status=1;
						self.searchItem.transport_status=2;
						self.searchItem.isremark=0
						self.searchItem.order_step=0
					}else if(self.status==6){
						self.searchItem.pay_status=1;
						self.searchItem.transport_status=2;
						self.searchItem.isremark=1
						self.searchItem.order_step=0
					}else if(self.status==7){
						delete self.searchItem.transport_status;
						delete self.searchItem.pay_status;
						delete self.searchItem.isremark;
						self.searchItem.order_step=['>',0]
					};
					self.getMainData(true)
				}
			},
			
			changeStatusTwo(statusTwo){
				const self = this;
				if(statusTwo!= self.statusTwo){
					self.statusTwo = statusTwo;
					if(self.statusTwo==1){
						delete self.searchItem.transport_status;
						delete self.searchItem.pay_status;
						delete self.searchItem.order_step;
						delete self.searchItem.isremark;
					}else if(self.statusTwo==2){
						self.searchItem.pay_status=0
					}else if(self.statusTwo==3){
						self.searchItem.pay_status=1;
						self.searchItem.transport_status=['in',[0,1]];
						self.searchItem.isremark=0
						self.searchItem.order_step=0
					}else if(self.statusTwo==4){
						self.searchItem.pay_status=1;
						self.searchItem.transport_status=2;
						self.searchItem.isremark=0
						self.searchItem.order_step=0
					}else if(self.statusTwo==5){
						self.searchItem.pay_status=1;
						self.searchItem.transport_status=2;
						self.searchItem.isremark=1
						self.searchItem.order_step=0
					}else if(self.statusTwo==6){
						delete self.searchItem.transport_status;
						delete self.searchItem.pay_status;
						delete self.searchItem.isremark;
						self.searchItem.order_step=['>',0]
					}
					self.getMainData(true)
				}
			},
			
			hxEwmShow(index){
				const self = this;
				
				if(index||index==0){
					self.chooseIndex = index
				};
				self.is_show = !self.is_show
				self.is_hxEwmShow = !self.is_hxEwmShow
			},
			
			getMainData(isNew) {
				const self = this;
				if (isNew) {
					self.mainData = [];
					self.paginate = {
						count: 0,
						currentPage: 1,
						is_page: true,
						pagesize: 10
					}
				};
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.searchItem = self.$Utils.cloneForm(self.searchItem);
				postData.searchItem.user_no = uni.getStorageSync('user_info').user_no;
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data);
					}
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
