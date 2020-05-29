<template>
	<view>
		
		<view class="banner-box">
			<swiper class="swiper-box" indicator-dots="true" autoplay="true" interval="3000" duration="1000" indicator-active-color="#757575">
				<block v-for="(item,index) in mainData.bannerImg" :key="index">
					<swiper-item class="swiper-item">
						<image :src="item.url" class="slide-image" />
					</swiper-item>
				</block>
			</swiper>
		</view>
		<view class="flexRowBetween pdt15">
			<view class="fs15 pdl15" style="width: 76%;">{{mainData.title?mainData.title:''}}</view>
			<button class="shareBtn flexCenter color9 fs12" open-type="share">
				<image style="width: 28rpx;height: 28rpx;" src="../../static/images/detailsl-icon.png" mode=""></image>
				<view class="mgl5">分享</view>
			</button>
		</view>
		<view class="mglr4 pdtb15">
			<view class="flex fs12 color9">
				<view class="mgr20">库存：{{mainData.stock?mainData.stock:'0'}}</view>
				<view>销量：{{mainData.sale_count?mainData.sale_count:'0'}}</view>
			</view>
			<view class="flex mgt10">
				<view class="fs15 ftw red mgr15">拼团价￥{{mainData.group_price?mainData.group_price:''}}</view>
				<view class="fs12 color6">市场价￥{{mainData.price?mainData.price:''}}</view>
			</view>
		</view>
		
		<view class="f5H5"></view>
		<view class="detail_join mglr4 pdtb15">
			<view class="flexRowBetween fs13">
				<view  v-if="groupData.length>0">{{groupData.length}}人正在拼团，可直接参与</view>
				<view  v-else>还没有人开团，快去开团吧</view>
				<view v-if="groupData.length>0" class="fs12 color9 flexEnd" @click="Router.navigateTo({route:{path:'/pages/pinDetail-pinMore/pinDetail-pinMore?id='+mainData.id}})">
					<view>查看更多</view>
					<image class="arrowR" style="width: 12rpx;height: 20rpx;" src="../../static/images/detailsl-icon2.png" mode=""></image>
				</view>
			</view>
			
			<view class="twolist">
				<view class="item flexRowBetween pdt15"  v-for="(item,index) in groupData">
					<view class="ll flex">
						<view class="photo">
							<image :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" mode=""></image>
						</view>
						<view class="tit color6 fs13 avoidOverflow">{{item.title}}</view>
					</view>
					<view class="rr flexRowBetween">
						<view class="downTime">
							<view class="fs12">还差<span class="red">{{item.lessNum}}人</span>拼成</view>
							<view class="fs10 color9">剩余{{countDownList[index].hou}}:{{countDownList[index].min}}:{{countDownList[index].sec}}</view>
						</view>
						<view class="go fs12" :data-group_no="item.group_no" @click="Router.navigateTo({route:{path:'/pages/orderConfim/orderConfim?isGroup=true&group_no='+$event.currentTarget.dataset.group_no}})">去拼团</view>
					</view>
				</view>
			</view>
		</view>
		
		<view class="f5H5"></view>
		
		<view class="mglr4 pdtb15  color6">
			<view class="flexRowBetween" @click="spaceShow">
				<view class="fs13">{{mainData.sku[specsCurr]?'已选'+mainData.sku[specsCurr].title:'选择商品规格'}}</view>
				<view class="arrowR"><image src="../../static/images/home-icon2.png" mode=""></image></view>
			</view>
		</view>
		<view class="f5H10"></view>
		
		<view class="orderNav flexRowBetween pdt5 ">
			<view class="tt flexCenter" :class="curr==1?'on':''" @click="changeCurr('1')">详细介绍</view>
			<view class="tt flexCenter" :class="curr==2?'on':''"  @click="changeCurr('2')">评论（{{messageData.length}}）</view>
		</view>
		
		<view class="pdt15" v-show="curr==1">
			<view class="mglr4 xqInfor">
				<view class="cont fs14">
					<view class="content ql-editor" style="padding:0;"
					v-html="mainData.content">
					</view>
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
								<view class="photo mgr5"><image :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:'../../static/images/about-img10.png'" mode=""></image></view>
								<view class="name color6">{{item.title!=''?item.title:item.user_no}}</view>		
							</view>
							<view class="time color9">{{item.description}}</view>
						</view>
						<view class="text fs13">{{item.description}}</view>
					</view>
				</view>
			</view>
		</view>
		<view class="xqbotomBar pdl15 center" style="height: 100rpx;">
			<view class="ite flexCenter fs12" style="width: 180rpx;">
				<view class="flexColumn" @click="addCar">
					<view class="">
						<image src="../../static/images/detailsl-icon1.png" mode=""></image>
					</view>
					<view class="mgt5">加入购物车</view>
				</view>
			</view>
			<view class="flexEnd">
				<view class="payBtn" style="width: 250rpx; background: #ffafcf;" @click="goBuy(false)">单独购买</view>
				<view class="payBtn"  style="width: 250rpx;" @click="goBuy(true)">开团</view>
			</view>
			
		</view>
		
		
		<!-- 规格选择 -->
		<view class="black-bj" v-show="is_show"></view>
		<view class="spaceShow whiteBj" v-show="is_spaceShow">
			<view class="closebtn" @click="spaceShow">×</view>
			<view class="flex">
				<view class="pic radius8 oh mgr15"><image :src="mainData.sku[specsCurr]&&mainData.sku[specsCurr].mainImg&&mainData.sku[specsCurr].mainImg[0]
					?mainData.sku[specsCurr].mainImg[0].url:''" mode=""></image></view>
				<view class="infor">
					<view class="price ftw fs18 mgt10 pdt10 mgb15">{{mainData.sku[specsCurr]?mainData.sku[specsCurr].price:''}}</view>
					<view class="fs13">请选择规格</view>
				</view>
			</view>
			<view class="mgt15">
				<view class="fs13">规格</view>
				
				<scroll-view class="specsLable flex fs13 color6" scroll-y="true" style="height: 360rpx;">
					<view class="tt" style="display: inline-block;" :class="specsCurr==index?'on':''" v-for="(item,index) in mainData.sku" :key="index"
					@click="specsChange(index)">{{item.title}}</view>
				</scroll-view>
			</view>
			<view class="xqbotomBar pdlr4 mgb15" style="box-shadow:initial;">
				<view class="bottom-btnCont flex d-flex radius10 oh white fs15 center" style="width: 100%;border-radius: 40rpx;">
					<view class="btn  hei" @click="addCar">加入购物车</view>
					<view class="btn pubBj" style="background: #ffafcf;" @click="goBuy(false)">单独购买</view>
					<view class="btn pubBj"  @click="goBuy(true)">开团</view>
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
				Utils:this.$Utils,
				mainData:{},
				curr:1,
				messageData:[],
				groupData:[],
				countDownList: [],
				endTimeList: [],
				canGroup:true,
		
				specsCurr:0,
				specsData:['定制版120ML','定制版100ML'],
				is_spaceShow:false,
				seltSpecsData:['定制版120ML','定制版100ML','定制版','定制版','定制版100ML','定制版120ML'],
				is_show:false
			}
		},
		
		onLoad(options) {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.id = options.id;
			self.$Utils.loadAll(['getMainData'], self);
		},
		
		onShow() {
			const self = this;
			self.orderList = [];
			uni.removeStorageSync('payPro');
		},
		
		onReachBottom() {
			console.log('onReachBottom')
			const self = this;
			if (!self.isLoadAll && uni.getStorageSync('loadAllArray')&&self.curr==2) {
				self.paginate.currentPage++;
				self.getMessageData()
			};
		},
		
		onShareAppMessage(ops) {
			console.log(ops)
			const self = this;
			if (ops.from === 'button') {
				
				return {
					title:self.mainData.title,
					path: '/pages/detail/detail?id='+self.id, //点击分享的图片进到哪一个页面
					imageUrl:self.mainData&&self.mainData.mainImg&&self.mainData.mainImg[0]&&self.mainData.mainImg[0].url?self.mainData.mainImg[0].url:'',
					success: function(res) {
						// 转发成功
						
						console.log("转发成功:" + JSON.stringify(res));
					},
					fail: function(res) {
						// 转发失败
						console.log("转发失败:" + JSON.stringify(res));
					}
				}
			}else{
				return {
					title:self.mainData.title,
					path: '/pages/detail/detail?id='+self.id, //点击分享的图片进到哪一个页面
					imageUrl:self.mainData&&self.mainData.mainImg&&self.mainData.mainImg[0]&&self.mainData.mainImg[0].url?self.mainData.mainImg[0].url:'',
					success: function(res) {
						// 转发成功
						
						console.log("转发成功:" + JSON.stringify(res));
					},
					fail: function(res) {
						// 转发失败
						console.log("转发失败:" + JSON.stringify(res));
					}
				}
			}
		},
		
		methods: {
			specsChange(index){
				const self = this;
				self.specsCurr = index
			},
			spaceShow(){
				const self = this;
				self.is_show = !self.is_show;
				self.is_spaceShow = !self.is_spaceShow 
			},
			changeCurr(curr){
				const self = this;
				if(curr!=self.curr){
					self.curr = curr
				}
			},
			
			goBuy(isGroup){
				const self = this;
				uni.setStorageSync('canClick',false);
				if(!self.mainData.sku[self.specsCurr]){
					uni.setStorageSync('canClick',true);
					self.$Utils.showToast('商品暂无规格！', 'none');
					return
				};
				
				if(isGroup){
					if(Date.parse(new Date())>parseInt(self.mainData.end_time)){
						uni.setStorageSync('canClick',true);
						uni.showModal({
							title:'提示',
							content:'限时特卖已结束，请单独购买',
							showCancel:false,
						})
						return
					}
					if(Date.parse(new Date())<parseInt(self.mainData.start_time)){
						uni.setStorageSync('canClick',true);
						uni.showModal({
							title:'提示',
							content:'限时特卖还未开始，请单独购买',
							showCancel:false,
						})
						return
					};
					self.orderList.push(
						{sku_id:self.mainData.sku[self.specsCurr].id,count:1,
						type:self.mainData.type,product:self.mainData,skuIndex:self.specsCurr},
					);
					uni.setStorageSync('payPro', self.orderList);
					self.Router.navigateTo({route:{path:'/pages/orderConfim/orderConfim?isGroup=true'}})
				}else{
					self.orderList.push(
						{sku_id:self.mainData.sku[self.specsCurr].id,count:1,
						type:self.mainData.type,product:self.mainData,skuIndex:self.specsCurr},
					);
					uni.setStorageSync('payPro', self.orderList);
					self.Router.navigateTo({route:{path:'/pages/orderConfim/orderConfim'}})
				}
				uni.setStorageSync('canClick',true);
			},
			
			
			addCar() {
				const self = this;
				var obj = self.mainData;
				self.mainData.skuIndex = self.specsCurr;
				var array = self.$Utils.getStorageArray('cartData');
				for (var i = 0; i < array.length; i++) {
					if (array[i].sku[array[i].skuIndex].id == self.mainData.sku[self.specsCurr].id) {
						var target = array[i]
					}
				}
				if (target) {
					target.count = target.count + 1
				} else {
					var target = self.mainData;
					target.count = 1;
					target.isSelect = true;
				}
				self.$Utils.showToast('加入成功,团购商品与其他商品一起购买恢复原价', 'none');
				self.$Utils.setStorageArray('cartData', target, 'id', 999);
			},
			
			
			
			getMainData() {
				const self = this;
				const postData = {};
				postData.searchItem = {
					thirdapp_id: 2,
					id: self.id
				};
				postData.getAfter = {
					sku: {
						tableName: 'Sku',
						middleKey: 'product_no',
						key: 'product_no',
						condition: '=',
						searchItem: {
							status: 1
						}
					},
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData = res.info.data[0];
						const regex = new RegExp('<img', 'gi');
						self.mainData.content = self.mainData.content.replace(regex, `<img style="max-width: 100%;height:auto;"`);
						self.getMessageData();
						self.getGroupData()
						if(Date.parse(new Date())<parseInt(self.mainData.end_time)){
							self.canGroup = false
						}
					}
					console.log('self.mainData', self.mainData)
					
				};
				self.$apis.productGet(postData, callback);
			},
			
			getGroupData() {
				var self = this;
				var now = Date.parse(new Date())/1000;
				var postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.paginate = {
					count: 0,
					currentPage: 1,
					is_page: true,
					pagesize: 2
				};
				postData.searchItem = {
					group_status: 1,
					user_type:0,
					product_id:self.mainData.id,
					group_leader: 'true',
					invalid_time: ['>', now],
					pay_status:1
				};
				postData.getAfter = {
					groupMember: {
						tableName: 'Order',
						middleKey: 'group_no',
						key: 'group_no',
						searchItem: {
							status: 1,
							pay_status: 1,
							level:1
							//group_leader:'false'
						},
						condition: '='
					},
				};
				var callback = function(res) {
					if (res.info.data.length > 0 && res.info.data[0]) {
						self.groupData.push.apply(self.groupData, res.info.data);
						for (var i = 0; i < self.groupData.length; i++) {
							self.endTimeList.push({
								actEndTime: self.groupData[i].invalid_time
							})
							self.groupData[i].lessNum = parseInt(self.groupData[i].standard) - parseInt(self.groupData[i].groupMember.length)
						};
						self.countDown();
					};
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.orderGet(postData, callback);
			},
			
			timeFormat(param) { //小于10的格式化函数
				const self = this;
				return param < 10 ? '0' + param : param;
			},
			
			countDown() { //倒计时函数
				// 获取当前时间，同时得到活动结束时间数组
				const self = this;
				let newTime = new Date().getTime()/1000;
				let endTimeList = self.endTimeList;
				let countDownArr = [];
				// 对结束时间进行处理渲染到页面
				for (var i = 0; i < self.endTimeList.length; i++) {
					let endTime = self.endTimeList[i].actEndTime;
					let obj = null;
					// 如果活动未结束，对时间进行处理
					if (endTime - newTime > 0) {
						let time = (endTime - newTime);
						// 获取天、时、分、秒
						let day = parseInt(time / (60 * 60 * 24));
						let hou = parseInt(time % (60 * 60 * 24) / 3600);
						let min = parseInt(time % (60 * 60 * 24) % 3600 / 60);
						let sec = parseInt(time % (60 * 60 * 24) % 3600 % 60);
						if (day > 0) {
							hou = hou + day * 24
						}
						obj = {
							hou: self.timeFormat(hou),
							min: self.timeFormat(min),
							sec: self.timeFormat(sec)
						}
					} else { //活动已结束，全部设置为'00'
						obj = {
							hou: '00',
							min: '00',
							sec: '00'
						}
					}
					countDownArr.push(obj);
			
				}
				// 渲染，然后每隔一秒执行一次倒计时函数
				self.countDownList = countDownArr;
			
				setTimeout(this.countDown, 1000);
			},
			
			getMessageData(isNew) {
				var self = this;
				if (isNew) {
					self.messageData = [];
					self.paginate = {
						count: 0,
						currentPage: 1,
						is_page: true,
						pagesize: 10
					}
				};
				var postData = {};
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.searchItem = {
					thirdapp_id: 2,
					type:1,
					product_no:self.mainData.product_no,
				};
				var callback = function(res) {
					if (res.info.data.length > 0 && res.info.data[0]) {
						self.messageData.push.apply(self.messageData, res.info.data);
					};
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.messageGet(postData, callback);
			},
			
		}
	};
</script>

<style>
	@import "../../assets/style/orderNav.css";
	@import "../../assets/style/detail.css";
	page{padding-bottom:140rpx;}
	
	.swiper-box {height: 750rpx;box-sizing: border-box;overflow: hidden;}
	.swiper-box swiper-item{width: 100%;box-sizing: border-box;overflow: hidden;}
	.swiper-box swiper-item image{width: 100%;height: 100%;box-sizing: border-box;}
	
	.orderNav .tt.on{font-weight: bold;}
	.orderNav .tt.on::after{bottom:6rpx;}
	
	.shareBtn{background: #F5F5F5;width: 120rpx;height: 44rpx;border-radius: 25rpx 0 0 25rpx;}
	
	.xqbotomBar{z-index: 45;}
	button{
		background: none;
		line-height: 1.5;
		margin-left: 0;
		margin-right: 0;

	}
	button::after{
		border: none;
	}
	.button-hover {
		color: #000000;
		background: none;
	}
	
	.bottom-btnCont{width: 520rpx;line-height: 80rpx;}
	.bottom-btnCont .btn{width: 50%;}
	.bottom-btnCont .hei{background-color: #3c3c3c;}
	
	.specsLable{flex-wrap: wrap;}
	.specsLable .tt{margin: 30rpx 50rpx 0 0;border: 1px solid #ddd;line-height: 60rpx;padding: 0 16rpx;border-radius:10rpx;}
	
	.specsLable .tt.on{background-color: #ffedf4;color: #fc73aa;border: 1px solid #fc73aa;}
	
	.spaceShow{width: 100%;border-radius: 20rpx 20rpx 0 0;position: fixed;left: 0;right: 0;bottom: 0;height: 800rpx;z-index: 50;padding: 30rpx;padding-bottom: 140rpx;box-sizing: border-box;}
	.spaceShow .pic{width: 210rpx;height: 210rpx;border: 1px solid #E1E1E1;}
	.spaceShow .pic image{width: 100%;height: 100%;}
	.arrowR image{width: 100%;height: 100%;}
</style>
