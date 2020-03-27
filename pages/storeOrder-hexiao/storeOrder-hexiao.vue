<template>
	<view>
		
		<view class="mglr4 pdt15">
			<view class="proRow">
				<view class="item">
					<view class="fs12 flexRowBetween mgb10">
						<view class="color9">交易时间：{{mainData.create_time}}</view>
						<view class="red">{{mainData.transport_status==0?'待核销':'已核销'}}</view>
					</view>
					<view class="flexRowBetween"  v-for="(item,index) in mainData.child">
						<view class="pic">
							<image :src="item.orderItem&&item.orderItem[0]&&item.orderItem[0].snap_product
							&&item.orderItem[0].snap_product.mainImg&&item.orderItem[0].snap_product.mainImg[0]?item.orderItem[0].snap_product.mainImg[0].url:''" mode=""></image>
						</view>
						<view class="infor">
							<view class="avoidOverflow2 fs13">{{item.orderItem&&item.orderItem[0]&&item.orderItem[0].snap_product
							&&item.orderItem[0].snap_product?item.orderItem[0].snap_product.title:''}}</view>
							<view class="B-price flexRowBetween">
								<view class="price">{{item.price?item.price:''}}</view>
								<view class="fs13">×{{item.price?item.count:''}}</view>
							</view>
						</view>
					</view>
				</view>
			</view>
			
			<view class="mgt20 pdlr4 pdt15 fs13 pdb15 whiteBj radius10">
				<view class="flex pdb10">
					<view class="mgr20 color6">姓名</view>
					<view>{{mainData.snap_address&&mainData.snap_address.name?mainData.snap_address.name:''}}</view>
				</view>
				<view class="flex">
					<view class="mgr20 color6">电话</view>
					<view>{{mainData.snap_address&&mainData.snap_address.phone?mainData.snap_address.phone:''}}</view>
				</view>
			</view>
		</view>
		<view class="submitbtn"  style="margin-top:160rpx;">
			<button class="btn" type="button" v-if="mainData.transport_status==0" @click="$Utils.stopMultiClick(orderUpdate)">确认核销</button>
			<button class="btn" type="button" v-if="mainData.transport_status==2">已核销</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				Utils:this.$Utils,
				mainData:{}
			}
		},
		
		onLoad(options) {
			const self = this;
			self.id = options.id;
			self.$Utils.loadAll(['getMainData'], self);
		},
		
		methods: {
			
			orderUpdate() {
				const self = this;
				uni.setStorageSync('canClick', false);
				const postData = {};
				postData.tokenFuncName = 'getStaffToken';
				postData.data = {
					transport_status:2,
				};
				postData.searchItem = {
					id:self.id,
					user_type:0
				};
				const callback = (data) => {
					uni.setStorageSync('canClick', true);
					if (data && data.solely_code == 100000) {
						self.$Utils.showToast('操作成功','none');
						setTimeout(function() {
							uni.navigateBack({
								delta:1
							})
						}, 1000);
					} else {
						self.$Utils.showToast(data.msg,'none')
					}
				};
				self.$apis.orderUpdate(postData, callback);
			 },
			
			getMainData() {
				const self = this;
				console.log('852369')
				const postData = {
					searchItem:{
						id:self.id,
						user_type:0
					}
				};
				postData.tokenFuncName = 'getStaffToken'
				const callback = (res) => {
					if (res.solely_code == 100000 && res.info.data[0]) {
						self.mainData = res.info.data[0];
					} else {
						self.$Utils.showToast(res.msg, 'none');
						setTimeout(function() {
							uni.navigateBack({
								delta:1
							})
						}, 1000);
					};
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.orderGet(postData, callback);
			},
			
		}
	};
</script>

<style>
	@import "../../assets/style/proList.css";
	page{background: #F5F5F5;}
	
	.proRow .item .pic{width: 160rpx;height: 160rpx;}
	.proRow .item .infor{width: 72%;height: 160rpx;}
	
	textarea{color: #222;padding: 30rpx;}
</style>
