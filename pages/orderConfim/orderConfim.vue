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
							<view class="editMsg"><input type="text" value="" placeholder="请输入姓名" placeholder-class="placeholder" /></view>
							<view class="editMsg"><input type="text" value="" placeholder="请输入姓名" placeholder-class="placeholder" /></view>
						</view>
						<view class="pdt15">自提地址：雁塔区高新大都荟B座1009</view>
					</view>
				
					<view class="flexRowBetween" v-show="curr==2"  @click="Router.navigateTo({route:{path:'/pages/user_address/user_address'}})">
						<view class="fs14 color6">
							<view class="flex mgt5">
								<view class="mgr15 color2">张思德</view>
								<view>15689562352</view>
							</view>
							<view class="mgt5">陕西省西安市雁塔区高新大都荟</view>
						</view>
						<view class="flexEnd" style="width: 20%;">
							<image class="arrowR" src="../../static/images/home-icon2.png" mode=""></image>
						</view>
					</view>
					
					<view class="flexRowBetween" v-show="curr==3">
						<view class="fs14 color6">
							<view class="flex mgt5">
								<view class="mgr15 color2">唐久便利</view>
								<view>15689562352</view>
							</view>
							<view class="mgt5">西安市莲湖区糜家桥72号（搬到27号）</view>
						</view>
						<view class="flexEnd" style="width: 20%;">
							<image class="arrowR" src="../../static/images/home-icon2.png" mode=""></image>
						</view>
					</view>
					
				</view>
			</view>
			<view class="proRow mgt15">
				<view class="item flexRowBetween borderB1" >
					<view class="pic"><image src="../../static/images/submit-ordersl-img.png" mode=""></image></view>
					<view class="infor">
						<view class="tit">好孩子儿童餐具宝宝学吃饭</view>
						<view class="flexRowBetween B-price">
							<view class="price ftw">56</view>
							<view class="flexEnd">
								<view class="numBox flex">
									<view class="btn" @click="counter('-')">-</view>
									<view class="num">{{count}}</view>
									<view class="btn pubBj white add" @click="counter('+')">+</view>
								</view>
							</view>
						</view>
					</view>
				</view>
			</view>
		</view>
		
		<view class="xqbotomBar">
			<view class="flex mgl15 fs13">总计：<view class="price fs14">178</view></view>
			<view class="payBtn">立即购买</view>
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
				count:1
			}
		},
		onLoad() {
			const self = this;
			//self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			currChange(curr){
				const self = this;	
				if(curr!=self.curr){
					self.curr = curr
				}
			},
			counter(type) {
				const self = this;			
				if (type == '+') {
					self.count++;
				} else {
					if (self.count > 1) {
						self.count--;
					}
				};			
				self.countTotalPrice();
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
	
	
</style>
