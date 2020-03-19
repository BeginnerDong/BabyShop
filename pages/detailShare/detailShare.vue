<template>
	<view>
		<view class="pr T-head pdb15">
			<view class="bj"><image src="../../static/images/postersl-icon.png" mode=""></image></view>
			<view class="mglr4 flex white cont mgt5" >
				<view class="backIcon mgr15" @click="pre()"><image src="../../static/images/arrowL.png" mode=""></image></view>
				<view class="fs16 ftw">母婴用品</view>
				<view class="xian mgl15 mgr15"></view>
				<view class="logo">
					<image src="../../static/images/postersl-img.png" mode=""></image>
				</view>
			</view>
		</view>
		
		<view class="pdlr4 ">
			<view class="flexCenter center">
				<view class="photo">
					<image style="width: 50rpx;height: 50rpx;" src="../../static/images/about-img1.png" mode=""></image>
				</view>
				<view class="fs12 mgl5">哆啦A梦向您推荐</view>
			</view>
			<view class="fs15 mgt5 ftw pdb10 center">“母乳实干 百摔不坏”</view>
			
			<view class="proPic">
				<image src="../../static/images/postersl-img1.png" mode=""></image>
			</view>
			
			<view class="flexRowBetween pdt25">
				<view class="" style="width: 65%;">
					<view class="fs16 red ftw">￥56</view>
					<view class="avoidOverflow2 mgt5 fs13">可么多么COMOTOMO新生儿宽口径硅胶奶瓶套装配奶嘴</view>
				</view>
				<view class="flexEnd">
					<image style="width: 130rpx;height: 130rpx;" src="../../static/images/postersl-img2.png" mode=""></image>
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
				wx_info:{},
				is_show:false
			}
		},
		onLoad() {
			const self = this;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			pre(){
				this.$router.go(-1);
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
	/* @import "../../assets/style/detail.css"; */
	page{padding-bottom:140rpx;}
	.bj image{width: 100%;height: 170rpx;}
	.backIcon image{width: 18rpx;height:32rpx;}
	.T-head .cont{position: absolute;top: 30rpx;right: 0;left: 0;}
	.xian{width: 1px;height:30rpx;background: #ffb6d4;}
	.logo image{width: 142rpx;height: 75rpx;}
	
	.proPic{width: 690rpx;height: 690rpx;box-sizing: border-box;border: 1px solid #eee;}
	.proPic image{width: 100%;height: 100%;}
</style>
