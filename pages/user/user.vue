<template>
	<view>
		
		<view class="userHead">
			<view class="bj"><image class="w" src="../../static/images/about-img.png" mode="widthFix"></image></view>
			<view class="infor pdlr4 white">
				<view class="center fs16" style="height: 88rpx;line-height: 88rpx;">我的</view>
				<view class="flex pdt20">
					<view class="photo" style="overflow: hidden;"><open-data type="userAvatarUrl"></open-data></view>
					<view style="width: 70%;">
						<view class="fs14 pdb5"><open-data type="userNickName"></open-data></view>
					</view>
				</view>
				
			</view>
		</view>
		
		<view class="pdlr4">
			<view class="userBox2 boxShaow radius10 whiteBj pdlr4">
				<view class="flexRowBetween pdt15 pdb10 borderB1">
					<view class="">我的订单</view>
					<view class="more flexEnd fs12 color9" @click="Router.navigateTo({route:{path:'/pages/userOrder/userOrder'}})">查看<image class="arrowR" src="../../static/images/detailsl-icon2.png" mode=""></image></view>
				</view>
				<view class="menu flexRowBetween color6 fs12 pdtb15 center">
					<view class="item" @click="Router.navigateTo({route:{path:'/pages/userOrder/userOrder'}})">
						<view class="icon">
							<image src="../../static/images/about-icon.png"></image>
						</view>
						<view>快递订单</view>
					</view>
					<view class="item" @click="Router.navigateTo({route:{path:'/pages/userOrder/userOrder'}})">
						<view class="icon">
							<image src="../../static/images/about-icon1.png"></image>
						</view>
						<view>自提订单</view>
					</view>
					<view class="item" @click="Router.navigateTo({route:{path:'/pages/userOrder/userOrder'}})">
						<view class="icon">
							<image src="../../static/images/about-icon2.png"></image>
						</view>
						<view>送货上门</view>
					</view>
				</view>
			</view>
			
		</view>
		
		<view class="myRowBetween fs13 mglr4 pdlr4 whiteBj radius10 boxShaow mgt15">
			<view class="item flexRowBetween" @click="Router.navigateTo({route:{path:'/pages/user_address/user_address'}})" >
				<view class="ll flex">
					<image class="icon" src="../../static/images/about-icon3.png" mode=""></image>
					<view>地址管理</view>
				</view>
				<view class="rr"><image class="arrowR" src="../../static/images/detailsl-icon2.png" mode=""></image></view>
			</view>
			<view class="item flexRowBetween" @click="Router.navigateTo({route:{path:'/pages/user-ContactUs/user-ContactUs'}})" >
				<view class="ll flex">
					<image class="icon" src="../../static/images/about-icon4.png" mode=""></image>
					<view>联系我们</view>
				</view>
				<view class="rr"><image class="arrowR" src="../../static/images/detailsl-icon2.png" mode=""></image></view>
			</view>
			<view class="item flexRowBetween" @click="Router.navigateTo({route:{path:'/pages/storeLogin/storeLogin'}})" >
				<view class="ll flex">
					<image class="icon" src="../../static/images/about-icon5.png" mode=""></image>
					<view>门店入口</view>
				</view>
				<view class="rr"><image class="arrowR" src="../../static/images/detailsl-icon2.png" mode=""></image></view>
			</view>
		</view>
			
		<!--底部tab键-->
		<view class="navbar">
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
				<view class="nav_img">
					<image src="../../static/images/nabar1.png" />
				</view>
				<view class="text">首页</view>
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
					<image src="../../static/images/nabar4-a.png" />
				</view>
				<view class="text this-text">我的</view>
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
				showView: false,
				score:'',
				wx_info:{}
			}
		},
		onLoad() {
			const self = this;
			//self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {


		},
	};
</script>

<style>
	@import "../../assets/style/editInfor.css";
	@import "../../assets/style/navbar.css";
	page{padding-bottom: 140rpx;background: #F5F5F5;}
	
	.userHead{box-sizing: border-box;position: relative;width: 100%;height: 420rpx;}
	.userHead .photo{width: 120rpx;height: 120rpx;border-radius: 50%;margin-right: 20rpx;border: 2px solid #ffecca;;box-sizing: border-box;}
	.userHead .infor{position: absolute;top: 20px; right: 0; left: 0;}
	
	.myRowBetween .ll .icon{width: 30rpx;height: 32rpx;margin-right: 20rpx;}
	
	
	.userBox2{width: 100%;height: 250rpx;box-sizing: border-box;margin-top: -90rpx;position: relative; z-index: 1; box-shadow: 0 10rpx 20rpx rgba(0,0,0,0.1);}
	.userBox2 .item{width: 30%;}
	.userBox2 .item .icon{width: 48rpx;height:48rpx;display: block;margin: 0 auto;margin-bottom: 10rpx;position: relative;}
	.userBox2 .item .icon image{width: 100%;height: 100%;}
	
</style>
