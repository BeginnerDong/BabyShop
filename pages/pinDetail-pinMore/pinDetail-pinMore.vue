<template>
	<view>
		
		<view class="detail_join mglr4">
			<view class="twolist">
				<view class="item flexRowBetween pdt15" v-for="(item,index) in pinData" :key="index">
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
				pinData:[{},{},{},{},{},{},{}]
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
	@import "../../assets/style/detail.css";
	
</style>
