<template>
	<view class="content">
		<qian-dao :list="list" :date="date" :time_key="time_key" @day_change="day_change_fun" @date_change="date_change_fun"></qian-dao>
	</view>
</template>

<script>
	// 签到
	import QianDao from "@/components/qian-dao/qian-dao.vue";
	export default {
		// 组件
		components: {
			// 签到
			QianDao,
		},
		data() {
			return {
				// 当前的日期
				date: "",

				// 存放时间的key值
				time_key: "",
				// 已经签到的数据列表
				list: ["2020-05-10", "03-15", "20", "31"],

				// // 存放时间的key值
				// time_key: "time",
				// // 已经签到的数据列表
				// list: [{
				// 	time: "2020-05-10",
				// }, {
				// 	time: "03-15",
				// }, {
				// 	time: "20",
				// }, {
				// 	time: "31"
				// }],
			}
		},
		onLoad() {

		},
		// 方法
		methods: {
			// 点击天
			day_change_fun(day) {
				console.log(JSON.parse(JSON.stringify(day)));

				// 存放时间的key值
				let time_key = this.time_key;

				// 如果没有签到（可以补签，需要补签的可以这么写）
				if (!day.click) {
					if (time_key) {
						let obj = {};
						obj[time_key] = day.nyr;
						this.list.push(obj);
					} else {
						this.list.push(day.nyr);
					}
				}

				// 如果今天没有签到(只签到今天的，如果只需要签到今天的可以这么写)
				// if (!day.click && day.type == "today") {
				// 	if (time_key) {
				// 		let obj = {};
				// 		obj[time_key] = day.nyr;
				// 		this.list.push(obj);
				// 	} else {
				// 		this.list.push(day.nyr);
				// 	}
				// }
			},
			// 日期改变时触发
			date_change_fun(date) {
				// 更新日期
				this.date = date;

				// 清空已经签到的列表
				this.list = [];

				// 根据日期获取已经签到的列表然后赋值
				// 存放时间的key值
				let time_key = this.time_key;
				if (time_key) {
					this.list.push({
						time: "01"
					});
				} else {
					this.list.push("01");
				}
			},
		},
	}
</script>

<style>
	.content {}
</style>
