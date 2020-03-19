<template>
	<view>
		
		<view class="banner-box">
			<swiper class="swiper-box" indicator-dots="true" autoplay="true" interval="3000" duration="1000" indicator-active-color="#757575">
				<block v-for="(item,index) in labelData" :key="index">
					<swiper-item class="swiper-item">
						<image :src="item" class="slide-image" />
					</swiper-item>
				</block>
			</swiper>
		</view>
		<view class="flexRowBetween pdt15">
			<view class="fs15 pdl15" style="width: 76%;">babycare奶瓶夹，奶瓶消毒夹耐高温硅胶防滑奶瓶夹子</view>
			<view class="shareBtn flexCenter color9 fs12" @click="Router.navigateTo({route:{path:'/pages/detailShare/detailShare'}})"><image style="width: 28rpx;height: 28rpx;" src="../../static/images/detailsl-icon.png" mode=""></image><view class="mgl5">分享</view></view>
		</view>
		<view class="mglr4 pdtb15">
			<view class="flex fs12 color9">
				<view class="mgr20">库存：2421</view>
				<view>销量：232</view>
			</view>
			<view class="flex mgt10">
				<view class="fs15 ftw red mgr15">拼团价￥88</view>
				<view class="fs12 color6">市场价￥125</view>
			</view>
		</view>
		
		<view class="f5H5"></view>
		<view class="detail_join mglr4 pdtb15">
			<view class="flexRowBetween fs13">
				<view>45人正在拼团，可直接参与</view>
				<view class="fs12 color9 flexEnd" @click="Router.navigateTo({route:{path:'/pages/pinDetail-pinMore/pinDetail-pinMore'}})">
					<view>查看更多</view>
					<image class="arrowR" style="width: 12rpx;height: 20rpx;" src="../../static/images/detailsl-icon2.png" mode=""></image>
				</view>
			</view>
			<view class="twolist">
				<view class="item flexRowBetween pdt15">
					<view class="ll flex">
						<view class="photo">
							<image src="../../static/images/detailsl-img2.png" mode=""></image>
						</view>
						<view class="tit color6 fs13 avoidOverflow">名称名称名称</view>
					</view>
					<view class="rr flexRowBetween">
						<view class="downTime">
							<view class="fs12">还差<span class="red">1人</span>拼成</view>
							<view class="fs10 color9">剩余23:23:48</view>
						</view>
						<view class="go fs12" @click="Router.navigateTo({route:{path:'/pages/orderConfim/orderConfim'}})">去拼团</view>
					</view>
				</view>
				<view class="item flexRowBetween pdt15">
					<view class="ll flex">
						<view class="photo">
							<image src="../../static/images/detailsl-img2.png" mode=""></image>
						</view>
						<view class="tit color6 fs13 avoidOverflow">名称名称名称</view>
					</view>
					<view class="rr flexRowBetween">
						<view class="downTime">
							<view class="fs12">还差<span class="red">1人</span>拼成</view>
							<view class="fs10 color9">剩余23:23:48</view>
						</view>
						<view class="go fs12" @click="Router.navigateTo({route:{path:'/pages/orderConfim/orderConfim'}})">去拼团</view>
					</view>
				</view>
			</view>
		</view>
		
		<view class="f5H5"></view>
		
		<view class="orderNav flexRowBetween pdt5 ">
			<view class="tt flexCenter" :class="curr==1?'on':''" @click="changeCurr('1')">详细介绍</view>
			<view class="tt flexCenter" :class="curr==2?'on':''"  @click="changeCurr('2')">评论（15）</view>
		</view>
		
		<view class="pdt15" v-show="curr==1">
			<view class="mglr4 xqInfor">
				<view class="cont fs14">
					<view>管理客服电话还房贷两个号和个梵蒂冈悲愤交加鹤骨鸡肤供货方点击可供货方都拉黑干活的放假开个会过分的话看刚发的刚发的个人个人赛退热贴热推监管科了付赛的价格过节费考虑到加工费</view>
					<view><image class="w" src="../../static/images/detailsl-img1.png" mode="widthFix"></image></view>
					<view>管理客服电话还房贷两个号和个梵蒂冈悲愤交加鹤骨鸡肤供货方点击可供货方都拉黑干活的放假开个会过分的话看刚发的刚发的个人个人赛退热贴热推监管科了付赛的价格过节费考虑到加工费</view>
				</view>
			</view>
		</view>
		
		<!-- 评价 -->
		<view class="pdlr4"  v-show="curr==2">
			<view class="detail_pjLis">
				<view class="item" v-for="(item,index) in messageData" :key="index">
					<view class="cont">
						<view class="flexRowBetween pdb10 fs12">
							<view class="flex">
								<view class="photo mgr5"><image src="../../static/images/detailsl-img2.png" mode=""></image></view>
								<view class="name color6">哆啦A梦</view>		
							</view>
							<view class="time color9">2020-03-17</view>
						</view>
						<view class="text fs13">根据瑞灵活赶紧来都搞好了电话沟通各环节的反馈给换了多个黑客帝国</view>
					</view>
				</view>
			</view>
		</view>
		<view class="xqbotomBar pdl15 center" style="height: 100rpx;">
			<view class="ite flexCenter fs12" style="width: 180rpx;">
				<view class="flexColumn">
					<view class="">
						<image src="../../static/images/detailsl-icon1.png" mode=""></image>
					</view>
					<view class="mgt5">加入购物车</view>
				</view>
			</view>
			<view class="flexEnd">
				<view class="payBtn" style="width: 250rpx; background: #ffafcf;" @click="Router.navigateTo({route:{path:'/pages/orderConfim/orderConfim'}})">单独购买</view>
				<view class="payBtn" style="width: 250rpx;" @click="Router.navigateTo({route:{path:'/pages/orderConfim/orderConfim'}})">开团</view>
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
				labelData: [
					"../../static/images/detailsl-img.png",
					"../../static/images/detailsl-img.png",
					"../../static/images/detailsl-img.png"
				],
				curr:1,
				messageData:[{},{},{},{}]
			}
		},
		onLoad() {
			const self = this;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			changeCurr(curr){
				const self = this;
				if(curr!=self.curr){
					self.curr = curr
				}
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
	@import "../../assets/style/orderNav.css";
	@import "../../assets/style/detail.css";
	page{padding-bottom:140rpx;}
	
	.swiper-box {height: 400rpx;box-sizing: border-box;overflow: hidden;}
	.swiper-box swiper-item{width: 100%;box-sizing: border-box;overflow: hidden;}
	.swiper-box swiper-item image{width: 100%;height: 100%;box-sizing: border-box;}
	
	.orderNav .tt.on{font-weight: bold;}
	.orderNav .tt.on::after{bottom:6rpx;}
	
	.shareBtn{background: #F5F5F5;width: 120rpx;height: 44rpx;border-radius: 25rpx 0 0 25rpx;}
	
	.xqbotomBar{z-index: 45;}
	

</style>
