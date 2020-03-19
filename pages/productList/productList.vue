<template>
	<view>
		
		<view class="">
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
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				is_show: false,
				wx_info:{},
				is_show:false,
				proData:[{},{},{},{},{}]
			}
		},
		onLoad() {
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
	@import "../../assets/style/proList.css";
	
	/* page{padding-bottom: 60rpx;}	 */
	
</style>
