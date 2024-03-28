<template>
	<swiper>
		<swiper-item v-for="(item,index) in majorData" :key="index">
			<view class="main">
				<view class="title">
					<img class="art-left" src="/static/images/common/return-left.png" alt="" />
					<text>{{item}}</text>
					<img class="art-right" src="/static/images/common/return-right.png" alt="" />
				</view>
				<view class="te">
					<view class="te-1" @click="exam(subject[index])" style="">
						<text>真题测试</text>
						
					</view>
					<view class="te-2">
						<text>错题本</text>
					</view>
					<view class="te-3">
						<text>历史题目</text>
					</view>
					<view class="te-4">
						<text>模拟测试</text>
					</view>
					<view class="te-5">
						<text>练习</text>
					</view>
					
				</view>
			</view>
			
			
		</swiper-item>
	</swiper>
</template>

<script>
	export default {
		data() {
			return {
				majorData:["数学","英语","计算机","政治"],
				subject:['examfunction','examfunction-english',"examfunction-computer","examfunction-politics"]
			}
		},
		methods: {
			exam(subject){
				uni.navigateTo({
					url:'/pages/test/exam?subject='+ subject
				})
			}
		}
	}
</script>

<style>
	@import url("@/style.css");
text{
	margin: 10px;
	font-size: 17px;
}
.main{
	height: auto;
	margin: 8px;
}
.title{
	height: 50px;
	box-shadow: 0 0 1px rgb(0,153,184) inset,0 0 2px rgb(0,153,184);
	background-color: white;
	display: flex;
	justify-content: space-around;
	align-items: center;
}

.art-right{
		height: 20px;
		width: 20px;
		
}
.art-left{
		height: 20px;
		width: 20px;
}
.te{
	top: 8px;
	display: flex;
	flex-wrap: wrap;
	align-items: center;
}
.te-1{
	margin: 13px;
	width: 150px;
	height: 150px;
	border-radius: 20px;
	background-image: url("../../static/images/common/1.png");
}
.te-2{
	margin: 13px;
	background-color: green;
	width: 150px;
	height: 150px;
	border-radius: 20px;
	background-image: url("../../static/images/common/2.png");
}
.te-3{
	margin: 13px;
	background-color: green;
	width: 150px;
	height: 150px;
	border-radius: 20px;
	background-image: url("../../static/images/common/3.png");
}
.te-4{
	margin: 13px;
	background-color: green;
	width: 150px;
	height: 150px;
	border-radius: 20px;
	background-image: url("../../static/images/common/4.png");
}
.te-5{
	margin: 13px;
	background-color: green;
	width: 150px;
	height: 150px;
	border-radius: 20px;
	background-image: url("../../static/images/common/5.png");
}
</style>
