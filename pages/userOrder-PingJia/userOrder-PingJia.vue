<template>
	<view>
		
		<view class="mglr4 pdt15">
			<view class="proRow">
				<view class="item">
					<view class="fs12 flexRowBetween mgb10">
						<view class="color9">交易时间：2020-01-18</view>
						<view class="red">已完成</view>
					</view>
					<view class="flexRowBetween">
						<view class="pic">
							<image src="../../static/images/the-orderl-img1.png" mode=""></image>
						</view>
						<view class="infor">
							<view class="avoidOverflow2 fs13">好孩子汤勺</view>
							<view class="B-price flexRowBetween">
								<view class="price">56.00</view>
								<view class="fs13">×1</view>
							</view>
						</view>
					</view>
				</view>
			</view>
			
			<view class="mgt20 pdb15">
				<view class="fs15">评价内容</view>
				<view class="mgt10 whiteBj radius10">
					<textarea value="" placeholder="写出您对它的评价,让更多的人知道~" placeholder-class="placeholder" />
				</view>
			</view>
		</view>
		<view class="submitbtn" style="margin-top:100rpx;">
			<button class="btn" type="button">确定</button>
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
				is_show:false
			}
		},
		onLoad() {
			const self = this;
			//self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
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
