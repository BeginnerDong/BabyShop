<template>
	<view>
		<view class="mglr4 mgt15">
			
			<view class="whiteBj radius10 mgb15">
				<view><image class="w" style="height: 8rpx;" src="../../static/images/submit-ordersl-icon.png" mode="widthFix"></image></view>
				<view class="pdlr4 pdt15 pdb15">
					<view class="flex seltTake center fs12 color6">
						<view class="btn" :class="curr==1?'on':''" @click="currChange('1')">门店自提</view>
						<view class="btn" :class="curr==2?'on':''" @click="currChange('2')">快递包邮</view>
						<view class="btn" :class="curr==3?'on':''" @click="currChange('3')">送货上门</view>
					</view>
				
					 <view class="" v-show="curr==1">
						<view class="flexRowBetween">
							<view class="editMsg"><input type="text" v-model="orderInfo.name" placeholder="请输入姓名" placeholder-class="placeholder" /></view>
							<view class="editMsg"><input type="number" maxlength="11" v-model="orderInfo.phone" placeholder="请输入电话" placeholder-class="placeholder" /></view>
						</view>
						<view class="pdt15">自提地址：{{shopAddress}}</view>
					</view>
				
					<view class="flexRowBetween" v-show="curr==2"  @click="Router.navigateTo({route:{path:'/pages/user_address/user_address'}})">
						<view class="fs14 color6" v-if="addressData.name">
							<view class="flex mgt5">
								<view class="mgr15 color2">{{addressData.name}}</view>
								<view>{{addressData.phone}}</view>
							</view>
							<view class="mgt5">{{addressData.city+addressData.detail}}</view>
						</view>
						<view class="fs14 color6" v-else>
							添加收货地址
						</view>
						<view class="flexEnd" style="width: 20%;">
							<image class="arrowR" src="../../static/images/home-icon2.png" mode=""></image>
						</view>
					</view>
					
					<view class="flexRowBetween" v-show="curr==3" @click="Router.navigateTo({route:{path:'/pages/user_address/user_address'}})">
						<view class="fs14 color6" v-if="addressData.name">
							<view class="flex mgt5">
								<view class="mgr15 color2">{{addressData.name}}</view>
								<view>{{addressData.phone}}</view>
							</view>
							<view class="mgt5">{{addressData.city+addressData.detail}}</view>
						</view>
						<view class="fs14 color6" v-else>
							添加收货地址
						</view>
						<view class="flexEnd" style="width: 20%;">
							<image class="arrowR" src="../../static/images/home-icon2.png" mode=""></image>
						</view>
					</view>
					
				</view>
			</view>
			<view class="proRow mgt15" v-for="(item,index) in mainData" :key="index">
				<view class="item flexRowBetween borderB1" >
					<view class="pic"><image :src="item.product&&item.product.mainImg&&item.product.mainImg[0]?item.product.mainImg[0].url:''" mode=""></image></view>
					<view class="infor">
						<view class="tit">{{item.product&&item.product.title?item.product.title:''}}</view>
						<view class="d-flex fs12 color6">
							<view class="specsBtn mr-1">{{item.product&&item.product.sku&&item.product.sku[item.skuIndex]?item.product.sku[item.skuIndex].title:''}}</view>
						</view>
						<view class="flexRowBetween B-price">
							<view class="price ftw" v-if="!isGroup">{{item.product&&item.product.sku&&item.product.sku[item.skuIndex]?item.product.sku[item.skuIndex].price:''}}</view>
							<view class="price ftw" v-if="isGroup">{{item.product&&item.product.sku&&item.product.sku[item.skuIndex]?item.product.sku[item.skuIndex].group_price:''}}</view>
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
			
			<view class="pdlr4 flexRowBetween whiteBj pdt15 pdb15 radius8 mgt15">
				<view>备注：</view>
				<view class="BZ-Text"><input type="text" v-model="passage1" placeholder="请输入备注信息" placeholder-class="" /></view>
			</view>
			
			
		</view>
		
		<view class="xqbotomBar">
			<view class="flex mgl15 fs13">总计：<view class="price fs14">{{totalPrice}}<span class="fs12">({{delivery>0?'含'+delivery+'元配送费':'已包邮'}})</span></view></view>
			<button class="payBtn" open-type="getUserInfo"  @getuserinfo="Utils.stopMultiClick(submit)">立即购买</button>
		</view>
		
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				showView: false,
				score:'',
				wx_info:{},
				is_show:false,
				curr:1,
				pay:{},
				totalPrice:0,
				mainData:[],
				orderInfo:{
					name:'',
					phone:''
				},
				shopAddress:'',
				shopLatitude:'',
				addressData:{},
				Utils:this.$Utils,
				isGroup:false,
				name:'',
				mainImg:[],
				passage1:'',
				delivery:0
			}
		},
		
		onLoad(options) {
			const self = this;
			if(options.isGroup){
				self.isGroup = options.isGroup
			};
			if(options.group_no){
				self.group_no = options.group_no
			};
			const callback = (res) => {
				self.$Utils.loadAll(['getUserData'], self);
				self.mainData = uni.getStorageSync('payPro');
				self.countTotalPrice()
			};
			self.$Token.getProjectToken(callback, {
				refreshToken: true
			})
			
		},
		
		onShow() {
			const self = this;
			if(uni.getStorageSync('choosedAddressData')){
				self.addressData = uni.getStorageSync('choosedAddressData')
				if(self.curr==3){
					self.checkDistance()
				}
			}else{
				self.getAddressData()
			};
		},
		
		
		
		methods: {
			
			checkDistance(){
				const self = this;
				if(self.addressData.latitude&&self.addressData.longitude){
					var distance = self.$Utils.distance(self.addressData.latitude,self.addressData.longitude,self.shopLatitude,self.shopLongitude);
					console.log('distance',distance);
					if(distance>parseFloat(uni.getStorageSync('user_info').thirdApp.distance)){
						uni.showModal({
						    title: '提示',
						    content: '该地址超出送货范围，请重新选择地址',
							confirmColor:'#FC73AA',
							showCancel:false,
						    success: function (res) {
						        if (res.confirm) {
						            self.addressData = {};
						        } else if (res.cancel) {
						           
						        }
						    }
						});	
					}
				}
			},
			
			getAddressData() {
				const self = this;		
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					isdefault:1
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.addressData = res.info.data[0];
					}
				};
				self.$apis.addressGet(postData, callback);
			},
			
			getUserData() {
				const self = this;
				const postData = {
					searchItem:{thirdapp_id:2}
				};
				postData.tokenFuncName = 'getProjectToken'
				postData.searchItem.user_no = uni.getStorageSync('user_info').user_no;
				const callback = (res) => {
					if (res.solely_code == 100000 && res.info.data[0]) {
						self.userInfoData = res.info.data[0];
						self.shopAddress = uni.getStorageSync('user_info').thirdApp.address;
						self.shopLatitude = uni.getStorageSync('user_info').thirdApp.latitude;
						self.shopLongitude = uni.getStorageSync('user_info').thirdApp.longitude;
					} else {
						self.$Utils.showToast(res.msg, 'none')
					};
					self.$Utils.finishFunc('getUserData');
				};
				self.$apis.userGet(postData, callback);
			},
			
			counter(index, type) {
				const self = this;
				if (type == '+') {
					self.mainData[index].count++;
				} else {
					if (self.mainData[index].count > 1) {
						self.mainData[index].count--;
					}
				};
				self.countTotalPrice();
			},
			
			countTotalPrice() {
				const self = this;
				self.totalPrice = 0;
				if(self.isGroup){
					for (var i = 0; i < self.mainData.length; i++) {
						self.totalPrice += self.mainData[i].product.sku[self.mainData[i].skuIndex].group_price*self.mainData[i].count
					}
				}else{
					for (var i = 0; i < self.mainData.length; i++) {
						self.totalPrice += self.mainData[i].product.sku[self.mainData[i].skuIndex].price*self.mainData[i].count
					}
				};
				
				self.totalPrice = parseFloat(self.totalPrice).toFixed(2)
				if(parseFloat(uni.getStorageSync('user_info').thirdApp.delivery_standard)>self.totalPrice){
					self.delivery = uni.getStorageSync('user_info').thirdApp.delivery_fee;
					self.totalPrice = (parseFloat(self.totalPrice)+parseFloat(uni.getStorageSync('user_info').thirdApp.delivery_fee)).toFixed(2)
				}else{
					self.delivery = 0;
					self.totalPrice = parseFloat(self.totalPrice).toFixed(2)
				}
				//console.log('wxPay',wxPay)
				if (self.totalPrice > 0) {
					self.pay.wxPay = {
						price: self.totalPrice,
					};
				} else {
					  delete self.pay.wxPay;	 
				};
				console.log(self.pay)
			},
			
			submit(){
				const self = this;
				uni.setStorageSync('canClick', false);
				if(self.curr==1){
					if(self.orderInfo.name==''||self.orderInfo.phone==''){
						uni.setStorageSync('canClick', true);
						self.$Utils.showToast('请填写收货人信息','none')
						return
					}
				}else{
					if(JSON.stringify(self.addressData) == '{}'){
						uni.setStorageSync('canClick', true);
						self.$Utils.showToast('请选择收货地址','none')
						return
					}
				};
				var data = {
					passage1:self.passage1
				};
				var orderList = []
				/* for (var i = 0; i < self.mainData.length; i++) {
					orderList.push({product_id:self.mainData[i].product_id,count:self.mainData[i].count,type:self.mainData[i].type})
				} */
				for (var i = 0; i < self.mainData.length; i++) {
					orderList.push({sku_id:self.mainData[i].sku_id,count:self.mainData[i].count,data: data,
					snap_address: self.addressData})
				}
				const callback = (user, res) => {
					self.name = user.nickName;
					self.mainImg = [{type:'image',url:user.avatarUrl}]
					self.addOrder(orderList)
				};
				self.$Utils.getAuthSetting(callback);
			},
			
			addOrder(orderList) {
				const self = this;	
				
				/* if(self.orderId){
					self.goPay()
					return
				}; */
				const postData = {}; 
				postData.orderList = self.$Utils.cloneForm(orderList);
				postData.data = {
					transport_type:self.curr,
					level:1,
					snap_address:self.addressData,
					name:self.name,
					mainImg:self.mainImg,
					passage1:self.passage1,
					price:self.pay.wxPay.price
				};
				postData.parent = 1;
				postData.tokenFuncName = 'getProjectToken';
				if(self.curr==1){
					postData.data.snap_address = {
						name:self.orderInfo.name,
						phone:self.orderInfo.phone
					}
				};
				if(self.isGroup){
					postData.isGroup = true;
					postData.data.standard = self.mainData[0].product.standard;
					postData.data.product_id = self.mainData[0].product.id;
					postData.data.invalid_time = parseInt(self.mainData[0].product.end_time)/1000
				};
				if(self.group_no){
					postData.group_no = self.group_no
				};
				const callback = (res) => {
					uni.setStorageSync('canClick', true);
					if (res && res.solely_code == 100000) {
						self.orderId = res.info.id;
						var array = self.$Utils.getStorageArray('cartData');
						for (var i = 0; i < orderList.length; i++) {
							for (var j = 0; j < array.length; j++) {
								if(orderList[i].sku_id == array[j].sku[array[j].skuIndex].id){
									self.$Utils.delStorageArray('cartData', orderList[i], 'id');
								}
							}
						};
						self.goPay()
					} else {		
						uni.showToast({
							title: res.msg,
							duration: 2000
						});
					};		
				};
				self.$apis.addOrder(postData, callback);
			},
			
			goPay() {
				const self = this;	
				const postData = self.$Utils.cloneForm(self.pay);	
				postData.tokenFuncName = 'getProjectToken',
				postData.searchItem = {
					id: self.orderId
				};
				const callback = (res) => {
					if (res.solely_code == 100000) {
						uni.setStorageSync('canClick', true);
					
						if (res.info) {
							const payCallback = (payData) => {
								console.log('payData', payData)
								if (payData == 1) {
									uni.showToast({
										title: '支付成功',
										duration: 1000,
										success: function() {
											
										}
									});
									setTimeout(function() {
										self.$Router.redirectTo({route:{path:'/pages/userOrder/userOrder'}})
									}, 1000);
								} else {
									uni.setStorageSync('canClick', true);
									uni.showToast({
										title: '支付失败',
										duration: 2000
									});
								};
							};
							self.$Utils.realPay(res.info, payCallback);
						} else {
							
							uni.showToast({
								title: '支付成功',
								duration: 1000,
								success: function() {
									
								}
							});
							setTimeout(function() {
								self.$Router.redirectTo({route:{path:'/pages/userOrder/userOrder'}})
							}, 1000);
						};
					} else {
						uni.setStorageSync('canClick', true);
						uni.showToast({
							title: res.msg,
							duration: 2000
						});
					};
				};
				self.$apis.pay(postData, callback);
			},
			
			currChange(curr){
				const self = this;	
				if(curr!=self.curr){
					self.curr = curr
					if(self.curr==3){
						self.checkDistance()
					}
				}
			},
			
		}
	};
</script>

<style>
	@import "../../assets/style/detail.css";
	@import "../../assets/style/proList.css";
	page{background: #F5F5F5;}
	
	.editMsg{width: 45%;height: 60rpx;padding: 0 10rpx;box-sizing: border-box;border: 1px solid #eee;box-sizing: border-box;text-align: center;}
	.editMsg input{width: 100%;height: 60rpx;line-height: 60rpx;box-sizing: border-box;text-align: center;font-size: 26rpx;}
	
	.seltTake .btn{width: 140rpx;height: 44rpx;line-height: 44rpx;border-radius: 30rpx;border: 1px solid #eee;margin: 0 30rpx 30rpx 0;}
	.seltTake .btn.on{color: #FC73AA;border-color: #FC73AA;}
	
	.proRow .item .pic{width: 140rpx; height: 140rpx;}
	.proRow .item .infor{width: 75%; height: 140rpx;}
	button{
		background: none;
		line-height: 1.5;
		margin-left: 0;
		margin-right: 0;
		font-size: 14px;
		border-radius: 0;
	}
	button::after{
		border: none;
	}
	.button-hover {
		color: #000000;
		background: none;
	}
	
	.BZ-Text{width: 75%;}
	.BZ-Text input{width: 100%;height: 60rpx;line-height: 60rpx;box-sizing: border-box;text-align: center;font-size: 26rpx;text-align: right;}
</style>
