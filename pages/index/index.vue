<template>
	<view>
		
		<view class="homeHead">
			<view class=""><image class="bj" src="../../static/images/home-icon4.png" mode=""></image></view>
			<view class="Hcont">
				<view class="seachbox">
					<view class="flex rr" style="width: 100%;" @click="Router.navigateTo({route:{path:'/pages/seach/seach'}})">
						<button class="seachBtn" type="button"><image src="../../static/images/home-icon.png" mode=""></image></button>
						<view class="input">
							<input type="text" name="" value="" placeholder="活动" placeholder-class="placeholder" />
						</view>
					</view>
				</view>
				<view class="banner-box pdlr4">
					<view class="banner">
						<swiper class="swiper-box" indicator-dots="true" autoplay="true" interval="3000" duration="1000" indicator-active-color="#757575">
							<block v-for="(item,index) in labelData" :key="index">
								<swiper-item class="swiper-item">
									<image :src="item" class="slide-image" />
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
					<view class="item" v-for="(item,index) in hotData" :key="index" @click="Router.navigateTo({route:{path:'/pages/detail/detail'}})">
						<view class="pic"><image src="../../static/images/home-img.png" mode=""></image></view>
						<view class="tit fs12 avoidOverflow2">好孩子儿童餐具宝宝学吃饭</view>
						<view class="price ftw">56</view>
					</view>
				</view>
			</view>
			
			<view class="fs15 ftw flex pdtb15" style="align-items: flex-start;">
				<view class="xian pubBj mgt5 mgr5" style="width: 4rpx;height: 14rpx;"></view>限时特卖
			</view>
			<view class="specialPro">
				<view class="item radius10 oh" v-for="(item,index) in specialProData" :key="index" @click="Router.navigateTo({route:{path:'/pages/pinDetail/pinDetail'}})">
					<view class="pic">
						<image src="../../static/images/home-img1.png" mode=""></image>
					</view>
					<view class="infor">
						<view class="tit fs15 mgb15">babycare奶瓶夹 奶瓶消毒夹高温硅胶防滑奶瓶夹子</view>
						<view class="flex">
							<view class="red mgr15 fs15 ftw">拼团价￥88</view>
							<view class="fs12 color6">市场价￥125</view>
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
				is_show: false,
				wx_info:{},
				is_show:false,
				labelData: [
					"../../static/images/home-banner.png",
					"../../static/images/home-banner.png",
					"../../static/images/home-banner.png"
				],
				hotData:[{},{},{}],
				specialProData:[{},{},{}]
			}
		},
		onLoad() {
			const self = this;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			call(){
				uni.makePhoneCall({
					phoneNumber:'15802977845'
				});
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
</style>
