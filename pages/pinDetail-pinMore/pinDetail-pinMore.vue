<template>
	<view>
		
		<view class="detail_join mglr4">
			<view class="twolist">
				<view class="item flexRowBetween pdt15"  v-for="(item,index) in mainData">
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
				pinData:[{},{},{},{},{},{},{}],
				mainData:[],
				countDownList: [],
				endTimeList: [],
			}
		},
		
		onLoad() {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.$Utils.loadAll(['getMainData'], self);
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
					group_status: 2,
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
				const callback = (res) => {
					if (res.info.data.length > 0 && res.info.data[0]) {
						self.mainData.push.apply(self.mainData, res.info.data);
						for (var i = 0; i < self.mainData.length; i++) {
							self.endTimeList.push({
								actEndTime: self.mainData[i].invalid_time
							})
							self.mainData[i].lessNum = parseInt(self.mainData[i].standard) - parseInt(self.mainData[i].groupMember.length)
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
		}
	};
</script>

<style>
	@import "../../assets/style/detail.css";
	
</style>
