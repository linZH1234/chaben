<template>
	<view>
		<JCalendar :yearMonth="targetDate" :dataSource="signData" @dateChange="getData" @clickChange="clickSign">
		</JCalendar>
		<!-- <view class="TipArea ">

		 </view> -->
		<view class='count'>
			<text>截至目前，已坚持打卡</text>
			<view class='daynumber'>
				<text class='number'>{{sumCount}}</text>
				<text class='day'>天</text>
			</view>

			<view>本月累积打卡<text class="monthSum">{{signData.length}}</text>天</view>
			<text>请再接再厉，继续努力!</text>
		</view>
	</view>
</template>

<script>
	import JCalendar from '@/components/j-calendar.vue';

	export default {
		data() {
			return {
				targetDate: parseInt(new Date().getFullYear()) + "-" + parseInt(new Date().getMonth() + 1), //本月
				sumCount: 0,
				signData: []
			};
		},
		components: {
			JCalendar
		},
		created() {
			//获取当前用户当前任务的签到状态
			this.getData(this.targetDate);
		},
		onLoad() {
			this.openid = wx.getStorageSync('openid');
		},
		methods: {
			async clickSign(day) {
				this.signData.push(day);
				this.sumCount++
				
				const res = await uniCloud.callFunction({
					name: "sign",
					data: {
						day: day,
						openid:wx.getStorageSync('openid')
					}
				}).then(res => {
					console.log(res)
				});
				if (res != undefined) {
					uni.showToast({
						title:day,
						icon: 'success',
						duration: 2000
					})

				}
			},
			unique(arr) {
			    if (!Array.isArray(arr)) {
			        console.log('type error!')
			        return
			    }
			    var array =[];
			    for(var i = 0; i < arr.length; i++) {
			            if( !array.includes( arr[i]) ) {//includes 检测数组是否有某个值
			                    array.push(arr[i]);
			              }
			    }
			    return array
			},
			//当模板的时候可以直接引入，然后触发子组件事件到父界面去控制数据

			//获取当前用户该任务的签到数组
		async getData(yearAndMonth) {
				const res = await uniCloud.callFunction({
					name: "getSign",
					data: {
						openid:wx.getStorageSync('openid')
					}
				}).then(res => {
					console.log(1)
					res = JSON.stringify(res.result.data)
					console.log(res)
					console.log(2)
				if (yearAndMonth === this.targetDate) {
					//这是我造的假数据！！！
					
					res = JSON.parse(res)

					const num2=[]
					for (let i = 0; i < res.length; i++) {
						num2.push(res[i].day.split('-')[2])
						let y = res[i].day.split('-')[0];
						let m = res[i].day.split('-')[1];
					}
					
					const num = Array.from(new Set(num2));
					console.log(num)
					const newSign = [],
					today = new Date().getDate();
					for (let i = 0; i < num.length; i++) {
						if (parseInt(num[i]) > today) { // 过滤掉今天之后的日子
							break;
						}
						newSign.push(this.targetDate + "-" + num[i])
					}
					// console.log(newSign);//-------------最后传给组件的格式看这里
					this.signData = newSign;
					console.log("signData")
					console.log(this.signData)
				} else {
					this.signData = [];
				}

				})
			},
		}
	}
</script>

<style>
	.count .daynumber {
		display: flex;
		flex-direction: row;
		justify-content: center;
	}

	.count .daynumber .day {
		margin-top: 50rpx;
	}

	.count {
		margin: 20rpx;
		padding: 30rpx;
		display: flex;
		text-align: center;
		border-radius: 10px;
		flex-direction: column;
		justify-content: center;
		background-color: #fff;
		align-items: center;
	}

	.count .number {
		color: #fff;
		font-size: 60rpx;
		background-color: #94db98;
		width: 100rpx;
		height: 100rpx;
		border-radius: 50%;
		display: flex;
		flex-direction: column;
		justify-content: center;
		margin: 20rpx;
	}

	.monthSum {
		color: red;
		font-size: 40rpx;
	}

	.count text {
		margin: 10rpx;
	}

	.TipArea {
		word-break: break-all;
		word-wrap: break-word;

		font-size: 14px;
		padding: 10px;
	}

	.impTip {
		display: inline-block;
		color: #ff0000;
	}
</style>