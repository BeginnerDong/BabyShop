<template>
	<view>
		
		<view class="mglr4">
			<view class=" pdtb15 flexRowBetween">
				<view>全部宝贝(3)</view>
				<view class="fs13"  v-show="!is_allDelt" @click="allDeltShow">管理</view>
				<view class="fs13"  v-show="is_allDelt" @click="allDeltShow">完成</view>
			</view>
			
			 <view class="proRow">
			 	<view class="item flexRowBetween borderB1" v-for="(item,index) in proListDate" :key="index">
					<view class="item_selBtn flex">
						<image class="seltIcon" src="../../static/images/shopping-icon2.png" mode=""></image>
					</view>
					<view class="R_cont flexRowBetween">
						<view class="pic"><image src="../../static/images/submit-ordersl-img.png" mode=""></image></view>
						<view class="infor">
			 			<view class="tit fs13">好孩子儿童餐具宝宝学吃饭</view>
							<view class="flexRowBetween B-price">
								<view class="price ftw">56</view>
								<view class="flexEnd">
									<view class="numBox flex">
										<view class="btn" @click="counter(index,'-')">-</view>
										<view class="num">{{item.count}}</view>
										<view class="btn pubBj white add" @click="counter(index,'+')">+</view>
									</view>
								</view>
							</view>
						</view>
					</view>
				</view>
			 </view>
			 <!-- 无数据 -->
			 <view class="nodata"><image src="../../static/images/nodata.png" mode=""></image></view>
		</view>
		
		
		<!-- 底部结算 -->
		<view class="xqbotomBar flexRowBetween borderB1 pdl15"  style="bottom: 110rpx;">
			<view class="left flex fs13">
				<view class="">
					<image class="seltIcon mgr5" src="../../static/images/shopping-icon2.png" mode=""></image>
				</view>
				<view>全选</view>
			</view>
			<view class="flexEnd">
				<view class="fs12 mgr15 flexEnd">合计<view class="price fs14">178</view></view>
				<view class="payBtn fs16 white" style="width: 260rpx;"  @click="Router.navigateTo({route:{path:'/pages/orderConfim/orderConfim'}})">结算</view>
			</view>
			
		</view>
		
		<!-- 底部全选删除 -->
		<view class="xqbotomBar flexRowBetween borderB1" v-show="is_allDelt" style="bottom: 110rpx;z-index: 100;">
			<view class="left flexRowBetween"  style="width: 66%;">
				<view class="flex color6 mgl10">
					<image class="seltIcon mgr5" src="../../static/images/shopping-icon2.png" mode=""></image>
					全选
				</view>
			</view>
			<view class="pubColor flexEnd mgr15" style="width: 34%;"><view class="alldeltBtn">删除</view></view>
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
					<image src="../../static/images/nabar3-a.png" />
				</view>
				<view class="text this-text">购物车</view>
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
				showView: false,
				wx_info:{},
				is_show:false,
				count:1,
				proListDate:[
					{price:'59.00',count:'1'},
					{price:'59.00',count:'1'}
				],
				is_allDelt:false
			}
		},
		
		onLoad(options) {
			const self = this;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			allDeltShow(){
				const self = this;
				self.is_allDelt = !self.is_allDelt
			},
			counter(index,type) {
				const self = this;
				if (type == '+') {
					self.proListDate[index].count++;
				} else {
					if (self.proListDate[index].count > 1) {
						self.proListDate[index].count--;
					}
				};
				self.$Utils.setStorageArray('cartData', self.proListDate[index], 'id', 999);
				self.countTotalPrice();
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
	@import "../../assets/style/proList.css";
	@import "../../assets/style/detail.css";
	
	page{padding-bottom: 240rpx;background: #F5F5F5;}
	
	
	.proRow .item{margin-bottom: 30rpx; align-items: center;}
	.proRow .item .pic{width: 140rpx; height: 140rpx;}
	.proRow .item .infor{height: 140rpx;width: 73%;}
	
	.proRow .item .R_cont{width: 90%; align-items: flex-start;}
	
	/* 商城商品列表 */
	.item_selBtn{width: 10%;}
	.seltIcon{width:36rpx; height: 36rpx; display: block;}
	/* .shopIcon{width: 27rpx; height: 24rpx; display: block;} */
	.alldeltBtn{width: 150rpx;height: 50rpx;line-height: 50rpx;border-radius: 30rpx;text-align: center;border:1px solid #FC73AA;}
	
	.xqbotomBar{height: 100rpx; z-index: 40;}
</style>
