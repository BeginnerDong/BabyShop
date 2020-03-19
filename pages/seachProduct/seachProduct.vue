<template>
	<view>
		<!-- 搜索 -->
		<view class="seachbox flexRowBetween whiteBj borderB1"  style="padding-bottom: 30rpx;"> 
			<view class="flex rr" style="width: 85%;">
				<button class="seachBtn" type="button">
					<image src="../../static/images/home-icon.png" mode=""></image>
				</button>
				<view class="input">
					<input type="text" name="" value="" placeholder="奶粉" placeholder-class="placeholder" />
				</view>
				<view class="delt flexCenter"><text>×</text></view>
			</view>
			<view class="fs15 pubColor" @click="Router.navigateTo({route:{path:'/pages/seachProduct/seachProduct'}})">搜索</view>
		</view>
		
		<view class="proRow mgt15">
			<view class="item flexRowBetween borderB1" v-for="(item,index) in productData" :key="index" @click="Router.navigateTo({route:{path:'/pages/detail/detail'}})">
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
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				showView: false,
				wx_info:{},
				is_show:false,
				productData:[{},{},{},{},{}]
			}
		},
		
		onLoad(options) {
			const self = this;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
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
	@import "../../assets/style/seach.css";
	@import "../../assets/style/prolist.css";
	page{padding-bottom: 60rpx;}
	
</style>

