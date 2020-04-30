<template>
	<view>
		
		<view class="mglr4 pdt15">
			<view class="proRow">
				<view class="item">
					<view class="fs12 flexRowBetween mgb10">
						<view class="color9">交易时间：{{mainData.order_no?mainData.order_no:''}}</view>
						<view class="red">已完成</view>
					</view>
					<view class="flexRowBetween">
						<view class="pic">
							<image :src="mainData.orderItem&&mainData.orderItem[0]&&mainData.orderItem[0].snap_product
							&&mainData.orderItem[0].snap_product.mainImg&&mainData.orderItem[0].snap_product.mainImg[0]?mainData.orderItem[0].snap_product.mainImg[0].url:''" mode=""></image>
						</view>
						<view class="infor">
							<view class="avoidOverflow2 fs13">{{mainData.title?mainData.title:''}}</view>
							<view class="B-price flexRowBetween">
								<view class="price">{{mainData.price?mainData.price:''}}</view>
								<view class="fs13">×{{mainData.count?mainData.count:''}}</view>
							</view>
						</view>
					</view>
				</view>
			</view>
			
			<view class="mgt20 pdb15">
				<view class="fs15">评价内容</view>
				<view class="mgt10 whiteBj radius10">
					<textarea v-model="submitData.description" placeholder="写出您对它的评价,让更多的人知道~" placeholder-class="placeholder" />
				</view>
			</view>
		</view>
		<view class="submitbtn" style="margin-top:100rpx;">
			<button class="btn" type="button" @click="Utils.stopMultiClick(submit)">确定</button>
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
				submitData: {
					order_no: '',
					product_no: '',
					description: '',
					type:1,
					title:'',
					mainImg:[],
					//passage1:'',
					thirdapp_id:2
				},
			}
		},
		
		onLoad(options) {
			const self = this;
			self.id = options.id;
			var res = self.$Token.getProjectToken(function(){
				self.$Utils.loadAll(['getMainData'], self)
			});
			if(res){
				self.$Utils.loadAll(['getMainData'], self)
			};
			self.submitData.mainImg = [{type:'image',url:uni.getStorageSync('user_info').headImgUrl}];
			self.submitData.title = uni.getStorageSync('user_info').nickname
		},
		
		methods: {
			
			getMainData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					id: self.id,
				};
				postData.getAfter = {
					orderItem:{
						tableName:'OrderItem',
						middleKey:'order_no',
						key:'order_no',
						searchItem:{
							status:1
						},
						condition:'=',
						
					}
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData = res.info.data[0];
						self.submitData.order_no = self.mainData.order_no;
						//self.submitData.passage1 = self.mainData.parent_no;
						self.submitData.product_no = self.mainData.orderItem[0].snap_product.product_no
					};
					console.log('self.mainData', self.mainData)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.orderGet(postData, callback);
			},
			
			submit() {
				const self = this;
				uni.setStorageSync('canClick', false);
				var newObject = self.$Utils.cloneForm(self.submitData);
				delete newObject.mainImg;
				delete newObject.title;
				const pass = self.$Utils.checkComplete(newObject);
				console.log('pass', pass);
				console.log('self.submitData', self.submitData)
				if (pass) {
					self.messageAdd();
				} else {
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('请补全信息', 'none')
				};
			},
			
			messageAdd() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				
				postData.data = {};
				postData.data = self.$Utils.cloneForm(self.submitData);
				postData.saveAfter = [{
				  tableName:'Order',
				  FuncName:'update',
				  searchItem:{
				    id:self.id
				  },
				  data:{
				    isremark:1,
				  }
				}];
				const callback = (data) => {
			
					if (data.solely_code == 100000) {
			
						self.$Utils.showToast('评价成功', 'none')
						setTimeout(function() {
							self.$Router.redirectTo({route:{path:'/pages/userOrder/userOrder'}})
						}, 1000);
					} else {
						uni.setStorageSync('canClick', true);
						self.$Utils.showToast(data.msg, 'none', 1000)
					}
			
				};
				self.$apis.messageAdd(postData, callback);
			},
			
		}
	};
</script>


<style>
	@import "../../assets/style/proList.css";
	page{background: #F5F5F5;}
	
	.proRow .item .pic{width: 160rpx;height: 160rpx;}
	.proRow .item .infor{width: 72%;height: 160rpx;}
	
	textarea{color: #222;padding: 30rpx;}
</style>
