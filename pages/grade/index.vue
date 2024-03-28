<template>
	<view class="container">
		<text class="mark">{{mart}}分</text>
		<text class="tips">{{mart < 90? '很遗憾，考试不合格':'恭喜，本次考试合格'}}</text>
		<view class="navigation">
			<view>
				<text>{{questionsLeft}}</text>
				<text>未做题</text>
			</view>
			<view>
				<text>{{wrongQuestions}}</text>
				<text>错题</text>
			</view>
			<view>
				<image src="/static/kaoshi.png" mode="widthFix"></image>
				<text>重新考试</text>
			</view>
		</view>
	</view>
	<view class="container">
		<text class="mock-title">20次最好成绩</text>
		<view class="history-score" v-for="(item,index) in scoreHistory" :key="index">
			<text>{{item.score}}分</text>
			<text>{{item.time}}</text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				mart:0,
				questionsLeft:0,
				wrongQuestions:0,
				correctAnswers:0,
				scoreHistory:[]
			}
		},
		onLoad(event){
			const analyze = JSON.parse(event.data)
			this.mart = analyze.mart
			this.questionsLeft = analyze.questionsLeft
			this.wrongQuestions = analyze.wrongQuestions
			this.correctAnswers = analyze.correctAnswers
			
			uniCloud.callFunction({
				 name: "scoreupdate",
				 data: {
				   score:this.mart,
				   time:new Date().toJSON().substring(0, 10) + ' ' + new Date().toTimeString().substring(0,8)
				 }
			});
			
			uniCloud.callFunction({
				name:"score",
				
			}).then(res=>{
				this.scoreHistory = res.result.data;
			})
		},
		methods: {
			
		}
	}
</script>

<style>
	page{
		background-color: #f7f7f7;
	}
	text{
		display: block;
	}
	.container{
		background-color: #ffffff;
		border-radius: 10rpx;
		margin: 20rpx;
		padding: 20rpx;
	}
	.mark{
		text-align: center;
		color: #ec6655;
		font-size: 50rpx;
		font-weight: bold;
	}
	.tips{
		text-align: center;
		padding: 30rpx 0;
		font-weight: bold;
		font-size: 40rpx;
	}
	.navigation{
		display: flex;
		align-items: center;
		justify-content: space-around;
	}
	.navigation view{
		display: flex;
		flex-direction: column;
		align-items: center;
	}
	.navigation image{
		display: block;
		width: 50rpx;
	}
	.navigation text{
		padding: 5rpx 0;
	}
	.mock-title{
		font-size: 35rpx;
		font-weight: bold;
	}
	.history-score{
		display: flex;
		justify-content: space-between;
		padding: 25rpx 0;
		border-bottom: 1rpx solid #f4f4f4;
	}
	.history-score text:nth-child(1){
		color: #ec6655;
		font-weight: bold;
	}
</style>