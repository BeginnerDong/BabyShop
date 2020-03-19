<template>
	<view>
		
		<view class="flexRowBetween" style="align-items: flex-start;">
			<view class="leftNav center fs13">
				<view class="tt flexCenter" :class="curr==index?'on':''" v-for="(item,index) in classNavData" :key="index" @click="currNavChange(index)">{{item}}</view>
			</view>
			<view class="rightCont">
				<view class="proRow">
					<view class="item flexRowBetween borderB1" v-for="(item,index) in proData" :key="index" @click="Router.navigateTo({route:{path:'/pages/detail/detail'}})">
						<view class="pic"><image src="../../static/images/hotPro-img.png" mode=""></image></view>
						<view class="infor">
							<view class="tit">好孩子儿童餐具宝宝学吃饭</view>
							<view class="flex B-price">
								<view class="price ftw">56</view>
							</view>
						</view>
					</view>
				</view>
				<!-- 无数据 -->
				<view class="nodata"><image src="../../static/images/nodata.png" mode=""></image></view>
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
					<image src="../../static/images/nabar2-a.png" />
				</view>
				<view class="text this-text">分类</view>
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
				classNavData:['全部','宝宝奶粉','宝宝尿裤','营养保健','零食辅助','喂养工具','宝宝餐具'],
				proData:[{},{},{}],
				curr:0
			}
		},
		onLoad() {
			const self = this;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			currNavChange(index){
				const self = this;
				self.curr = index
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
	@import "../../assets/style/proList.css";
	@import "../../assets/style/navbar.css";
	
	/* page{padding-bottom: 60rpx;}	 */
	.leftNav{width: 160rpx;background: #f5f5f5;position: fixed;top: 120rpx;left: 0;bottom: 0;box-sizing: border-box;}
	.leftNav .tt{height: 90rpx; color: #4d4d4d;}
	.leftNav .tt.on{background: #fff;color: #FC73AA;font-weight: bold;position: relative;}
	.leftNav .tt.on:before{content: '';width: 6rpx;height: 30rpx;background: #FC73AA;position: absolute;top: 50%;left:0;transform: translateY(-50%);}
	.rightCont{width: 100%;box-sizing: border-box;padding-left: 160rpx;min-height:756rpx;}
	
	.proRow .item .infor{width: 63%;}
</style>
