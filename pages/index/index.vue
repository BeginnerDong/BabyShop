<template>
	<view>
		
		<view class="homeHead">
			<view class=""><image class="bj" src="../../static/images/home-icon4.png" mode=""></image></view>
			<view class="Hcont">
				<view class="seachbox">
					<view class="flex rr" style="width: 100%;" @click="Router.navigateTo({route:{path:'/pages/seach/seach'}})">
						<button class="seachBtn" type="button"><image src="../../static/images/home-icon.png" mode=""></image></button>
						<view class="input">
							<input type="text" disabled="true" name="" value="" placeholder="搜索商品" placeholder-class="placeholder" />
						</view>
					</view>
				</view>
				<view class="banner-box pdlr4">
					<view class="banner">
						<swiper class="swiper-box" indicator-dots="true" autoplay="true" interval="3000" duration="1000" indicator-active-color="#757575">
							<block v-for="(item,index) in labelData.mainImg" :key="index">
								<swiper-item class="swiper-item">
									<image :src="item.url" class="slide-image" />
								</swiper-item>
							</block>
						</swiper>
					</view>
				</view>
			</view>
		</view>
		
		<view class="R-fixIcon" @click="call()"><image src="../../static/images/home-icon3.png" mode=""></image></view>
		
		<view class="pdlr4">
			
			<view class="hotTab oh radius10 mgb10">
				<view class="name flexRowBetween">
					<view class="fs15 ftw white">热销商品</view>
					<view class="more fs12 center" @click="Router.navigateTo({route:{path:'/pages/productList/productList'}})">查看更多</view>
				</view>
				<view class="flex pdlr4 pdt15 pdb15 whiteBj">
					<view class="item" v-for="(item,index) in hotData" :key="index" :data-id="item.id"
					@click="Router.navigateTo({route:{path:'/pages/detail/detail?id='+$event.currentTarget.dataset.id}})">
						<view class="pic"><image :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" mode=""></image></view>
						<view class="tit fs12 avoidOverflow2">{{item.title}}</view>
						<view class="price ftw">{{item.price}}</view>
					</view>
				</view>
			</view>
			
			<view class="fs15 ftw flex pdtb15" style="align-items: flex-start;">
				<view class="xian pubBj mgt5 mgr5" style="width: 4rpx;height: 14rpx;"></view>限时特卖
			</view>
			<view class="specialPro">
				<view class="item radius10 oh" v-for="(item,index) in mainData" :key="index" :data-id="item.id"
				 @click="Router.navigateTo({route:{path:'/pages/pinDetail/pinDetail?id='+$event.currentTarget.dataset.id}})">
					<view class="pic">
						<image :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" mode=""></image>
					</view>
					<view class="infor">
						<view class="tit fs15 mgb15">{{item.title}}</view>
						<view class="flex">
							<view class="red mgr15 fs15 ftw">拼团价￥{{item.group_price}}</view>
							<view class="fs12 color6">市场价￥{{item.price}}</view>
						</view>
					</view>
				</view>
			</view>
			
		</view>
		
		<!--底部tab键-->
		<view class="navbar">
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
				<view class="nav_img">
					<image src="../../static/images/nabar1-a.png" />
				</view>
				<view class="text this-text">首页</view>
			</view>
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/classify/classify'}})" >
				<view class="nav_img">
					<image src="../../static/images/nabar2.png" />
				</view>
				<view class="text">分类</view>
			</view>
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/car/car'}})" >
				<view class="nav_img">
					<image src="../../static/images/nabar3.png" />
				</view>
				<view class="text">购物车</view>
			</view>
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/user/user'}})" >
				<view class="nav_img">
					<image src="../../static/images/nabar4.png" />
				</view>
				<view class="text">我的</view>
			</view>
		</view>
		<!--底部tab键 end-->
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				labelData:{},
				hotData:[],
				specialProData:[{},{},{}],
				mainData:[]
			}
		},
		
		onLoad() {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.$Utils.loadAll(['getLabelData','getHotData','getMainData'], self);
		},
		
		onReachBottom() {
			console.log('onReachBottom')
			const self = this;
			if (!self.isLoadAll && uni.getStorageSync('loadAllArray')) {
				self.paginate.currentPage++;
				self.getMainData()
			};
		},
		
		methods: {
			
			
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
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.searchItem = {
					thirdapp_id:2,
					category_id:1
				}
				postData.order = {
					listorder: 'desc'
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData,res.info.data)
					};
					self.$Utils.finishFunc('getMainData');	
				};
				self.$apis.productGet(postData, callback);
			},
			
			call(){
				uni.makePhoneCall({
					phoneNumber:'15802977845'
				});
			},
			
			getHotData() {
				var self = this;
				var postData = {};
				postData.paginate = {
					count: 0,
					currentPage: 1,
					is_page: true,
					pagesize: 3
				};
				postData.searchItem = {
					thirdapp_id: 2,
					category_id:['not in',[1]]
				};
				postData.order = {
					listorder:'desc'
				};
				var callback = function(res) {
					if (res.info.data.length > 0 && res.info.data[0]) {
						self.hotData = res.info.data
					};
					self.$Utils.finishFunc('getHotData');
				};
				self.$apis.productGet(postData, callback);
			},
			
			getLabelData() {
				var self = this;
				var postData = {};
				postData.searchItem = {
					thirdapp_id: 2,
					title:'首页轮播'
				};
				var callback = function(res) {
					if (res.info.data.length > 0 && res.info.data[0]) {
						self.labelData = res.info.data[0]
					};
					self.$Utils.finishFunc('getLabelData');
				};
				self.$apis.labelGet(postData, callback);
			},
		}
	};
</script>

<style>
	@import "../../assets/style/navbar.css";
	@import "../../assets/style/seach.css";
	
	page{padding-bottom: 140rpx;background: #F5F5F5;}	
	
	.homeHead{height: 470rpx;}
	.homeHead .bj{width: 100%;height: 317rpx;}
	.homeHead .Hcont{position: absolute;top: 0;right: 0;left: 0;}
	
	.swiper-box {height: 320rpx;box-sizing: border-box;overflow: hidden;border-radius: 10rpx;}
	.swiper-box swiper-item{width: 100%;box-sizing: border-box;overflow: hidden;}
	.swiper-box swiper-item image{width: 100%;height: 100%;box-sizing: border-box;}
	
	.R-fixIcon{width: 100rpx;height: 100rpx;position: fixed;bottom:30%;right: 30rpx;z-index: 66;}
	.R-fixIcon image{width: 100%;height: 100%;}
	
	/* 热销产品 */
	.hotTab {border-radius: 30rpx 30rpx 0 0;}
	.hotTab .name{padding: 0 4%;height: 90rpx;background: #e7bd71;}
	.hotTab .name .more{width: 140rpx;height: 46rpx;line-height: 46rpx;border-radius: 25rpx;text-align: center;
	color: #73551f;border: 1px solid #73551f;}
	.hotTab .item{width: 191rpx;height: 328rpx;margin-right: 30rpx;}
	.hotTab .item:nth-of-type(3){margin-right: 0;}
	.hotTab .item .pic image{width: 100%;height: 191rpx;}
	.hotTab .item .tit{line-height: 36rpx;height: 72rpx;margin: 14rpx 0 20rpx 0;overflow: hidden;}
	.hotTab .item .price{line-height: 30rpx;}
	
	/* 特价商品 */
	.specialPro .item{margin-bottom: 30rpx;background: #fff;}
	.specialPro .item .pic{width: 100%;height: 300rpx;}
	.specialPro .item .pic image{width: 100%;height: 100%;}
	.specialPro .item .infor{padding: 24rpx 4%;}
	button{
		background: none;
	}
	button::after{
		border: none;
	}
	.button-hover {
		color: #000000;
		background: none;
	}
</style>
