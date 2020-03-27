<template>
	<view>
		
		<view class="flexRowBetween" style="align-items: flex-start;">
			<view class="leftNav center fs13">
				<view class="tt flexCenter" :class="curr==-1?'on':''"  @click="currNavChange(-1)">全部</view>
				<view class="tt flexCenter" :class="curr==item.id?'on':''" v-for="(item,index) in labelData" 
				:key="index" @click="currNavChange(index)">{{item.title}}</view>
			</view>
			<view class="rightCont">
				<view class="proRow">
					<view class="item flexRowBetween borderB1" v-for="(item,index) in mainData" :data-id="item.id"
					:key="index" @click="Router.navigateTo({route:{path:'/pages/detail/detail?id='+$event.currentTarget.dataset.id}})">
						<view class="pic"><image :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" mode=""></image></view>
						<view class="infor">
							<view class="tit">{{item.title}}</view>
							<view class="flex B-price">
								<view class="price ftw">{{item.price}}</view>
							</view>
						</view>
					</view>
				</view>
				<!-- 无数据 -->
				<view class="nodata" v-if="mainData.length==0"><image src="../../static/images/nodata.png" mode=""></image></view>
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
				classNavData:['全部','宝宝奶粉','宝宝尿裤','营养保健','零食辅助','喂养工具','宝宝餐具'],
				proData:[{},{},{}],
				curr:-1,
				labelData:[],
				searchItem:{
					thirdapp_id:2,
					category_id:['not in',[1]]
				},
				mainData:[]
			}
		},
		
		onLoad() {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.$Utils.loadAll(['getLabelData','getMainData'], self);
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
			
			getLabelData() {
				var self = this;
				var postData = {};
				postData.searchItem = {
					thirdapp_id: 2,
					type:3,
					id:['not in',[1]]
				};
				var callback = function(res) {
					if (res.info.data.length > 0 && res.info.data[0]) {
						self.labelData.push.apply(self.labelData,res.info.data)
					};
					self.$Utils.finishFunc('getLabelData');
				};
				self.$apis.labelGet(postData, callback);
			},
			
			currNavChange(index){
				const self = this;
				if(index==-1){
					self.curr = -1;
					self.searchItem.category_id = ['not in',[1]]
				}else{
					if(self.curr!=self.labelData[index].id){
						self.curr = self.labelData[index].id;
						self.searchItem.category_id = self.labelData[index].id;
					}
				};
				self.getMainData(true)
			},
			
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
				postData.searchItem = self.$Utils.cloneForm(self.searchItem);
				postData.order = {
					listorder: 'desc'
				};
				postData.getLimit = ['content','bannerImg'];
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData,res.info.data)
					};
					self.$Utils.finishFunc('getMainData');	
				};
				self.$apis.productGet(postData, callback);
			},
			
		}
	};
</script>

<style>
	@import "../../assets/style/proList.css";
	@import "../../assets/style/navbar.css";
	
	/* page{padding-bottom: 60rpx;}	 */
	.leftNav{width: 160rpx;background: #f5f5f5;position: fixed;top: 0;left: 0;bottom: 0;box-sizing: border-box;}
	.leftNav .tt{height: 90rpx; color: #4d4d4d;}
	.leftNav .tt.on{background: #fff;color: #FC73AA;font-weight: bold;position: relative;}
	.leftNav .tt.on:before{content: '';width: 6rpx;height: 30rpx;background: #FC73AA;position: absolute;top: 50%;left:0;transform: translateY(-50%);}
	.rightCont{width: 100%;box-sizing: border-box;padding-left: 160rpx;min-height:756rpx;}
	
	.proRow .item .infor{width: 63%;}
</style>
