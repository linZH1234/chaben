<template>
	<progress :percent="percent" show-info stroke-width="10" active active-mode="forwards" />
	<swiper :current="swiperCurrent" @change="changeCurrent">
		<swiper-item v-for="(item,index) in topicData" :key="index">
			<view class="topic-area">
				<text>{{item.type === '101' ? '单选题':'多选题'}}</text>
				<text>{{item.examQuestion}}</text>
			</view>
			<!-- 单选题 -->
			<block v-if="item.type === '101'">
				<view class="select-answer" v-for="(itema,indexa) in item.options" :key="indexa">
					<text v-if="!itema.isCorrect">{{sequence[indexa]}}</text>
					<image v-if="itema.isCorrect" :src="itema.icon_url" mode="widthFix"></image>
					<text @click="judgment(index,indexa,itema.select_id,item.correct_id,itema.isCorrect)">{{itema.select}}</text>
				</view>
			</block>
			<!-- 多选题 -->
			<block v-if="item.type === '102'">
				<view class="select-answer" v-for="(itema,indexa) in item.options" :key="indexa">
					<text v-if="!itema.whetherSubmit" :class="multipTextStyle(itema.isCorrect)">{{sequence[indexa]}}</text>
					<image v-if="itema.whetherSubmit" :src="itema.icon_url" mode="widthFix"></image>
					<text @click="multipleChoice(index,indexa,itema.select_id,item.correct_id,itema.isCorrect,item.store_check_id)">{{itema.select}}</text>
				</view>
				
				<!-- 提交按钮 -->
				<button class="submit" v-if="!item.answered"
				 :type="item.store_check_id.length >=2 ? 'primary':'default'" 
				 :disabled="item.store_check_id.length >=2 ? false:true" @click="subMit(index,item.store_check_id,item.correct_id,item.options)">
				 确定</button>
			</block>
			<block v-if="item.answered">
				<!-- 正确答案 -->
				<view class="Correct-answer">
					<text>答案:</text>
					<text v-for="(itema,indexa) in item.correct_answer" :key="index">{{itema}}</text>
				</view>
				<!-- 题目解析 -->
				<view class="anaylze">
					<view class="analyze-title">
						<text></text>
						<text>题目解析</text>
					</view>
					<text user-select class="analyze-correct">{{item.analyze}}</text>
				</view>
			</block>

		</swiper-item>
	</swiper>
	<view class="bottom-area">
		<view class="bottom-left" @click="submitPaper = true">交卷 {{state.formattedTime}}</view>
		<view class="bottom-right">
			<view @click="showPopup = true">
				<text>1</text>
				<text>答对</text>
			</view>
			<view @click="showPopup = true">
				<text>2</text>
				<text>答错</text>
			</view>
			<view @click="showPopup = true">
				<text>{{currentOrder}}/{{topicData.length}}</text>
				<text>题板</text>
			</view>
		</view>
	</view>
	<!-- 题板弹窗 -->
	<page-container :show="showPopup" @beforeleave="showPopup = false" @clickoverlay="showPopup = false">
	
		<view class="popup-view">
			<view class="topic-number">
				<view>
					<text v-for="(item,index) in topicData.length" :key="index"
					:class="getTestStyle(index)"
					@click="numericalOrder(index)"
					>{{item}}</text>
				</view>
			</view>
		</view>
	</page-container>
	<!-- 题目不合格弹窗 -->
	<view class="below-standard" v-if="isCorrectAnswer">
		<view class="main-content">
			<text class="unqualified-title">成绩不合格</text>
			<text class="unqualified-alert">已答错5题，测试不及格</text>
			<view class="submit-button">
				<text @click="isCorrectAnswer = false">继续考试</text>
				<text @click="examCompleted">现在交卷</text>
			</view>
		</view>
	</view>
<!-- 	自主交卷 -->
	<view class="below-standard" v-if="submitPaper">
		<view class="main-content">
			<text class="unqualified-title">确认交卷</text>
			<view class="answer-data">
				<view class="">
					<text>{{topicData.length - (correntIndex.length + errorIndex.length)}}</text>
					<text>未答题数</text>
				</view>
				<view class="">
					<text>{{state.formattedTime}}</text>
					<text>剩余时间</text>
				</view>
				<view class="">
					<text>{{2*correntIndex.length}}</text>
					<text>考试得分</text>
				</view>
			</view>
			<view class="submit-button">
				<text @click="submitPaper = false">继续考试</text>
				<text @click="examCompleted">现在交卷</text>
			</view>
		</view>
		
	</view>
</template>

<script>
	// 存储题目顺序
	export default {
		data() {
			return {
				topicData:[],
				sequence:['A','B','C','D','E','F'],
				imgData:['/static/yes.png','/static/no.png'],
				// 存储答对题下标
				correntIndex:[],
				// 存储答错题下标
				errorIndex:[],
				//进度条进度值
				percent:0,
				//多选错误答案
				errorId:[],
				//滑块顺序
				swiperCurrent:0,
				//当前题目顺序
				currentOrder:1,
				//控制弹窗弹出
				showPopup:false,
				//显示交卷弹窗
				isCorrectAnswer:false,
				//自主交卷弹窗
				submitPaper:false,
				//倒计时
				state:{
					countdown:2700,
					formattedTime:'45:00',
					countdownInterval:null
				}
				
			}
		},
		watch: {
			//错题5次弹窗
		        errorIndex: {
		            // 监听数据 获取到数据里的数组数据
		        handler(errorIndex,newVal) {
		            if(newVal.length === 5){
						this.isCorrectAnswer = true
					}
		        },
		        deep: true, // 深度监听
		        },
				
		},
		onShow() {
			//倒计时调用
			this.countdownStarts()
			
			//打乱题目
			
		},
		//页面销毁定时器
		onUnload(){
			// this.examCompleted()
		},
		onLoad(option){
			clearInterval(this.state.countdownInterval)
			uniCloud.callFunction({
				name:option.subject,
			}).then(res=>{
				this.shuffeArray(res.result.data)
				this.topicData = res.result.data;
				
			})
		},
		methods: {
			examCompleted(){
				const obj = {
					mart:2 * this.correntIndex.length,
					questionsLeft:this.topicData.length - (this.correntIndex.length + this.errorIndex.length),
					wrongQuestions:this.errorIndex.length,
					correctAnswers:this.correntIndex.length
				}
				wx.redirectTo({
					url:'/pages/grade/index?data=' +JSON.stringify(obj)
				})
			},
			//随机打乱数据
			shuffeArray(array){
				for(let i = array.length-1;i>0;i--){
					const j = Math.floor(Math.random()*(i+1));
					[array[i],array[j]] = [array[j],array[i]]
				}
			},
			// 选择单选题
			judgment(index,indexa,select_id,correct_id,isCorrect){
				

				if(this.topicData[index].answered)return false
				if(correct_id.includes(select_id)){// 正确
					//更新当前答案图片为正确图片
					this.topicData[index].options[indexa].icon_url = this.imgData[0]
					//状态改为正确
					this.topicData[index].options[indexa].isCorrect = true
					//保存正确题目下标
					this.correntIndex.push(index)
					//取出正确答案顺序
					var sequenceData = this.sequence[indexa]
					//选择正确自动 进入下一题
					 if(this.swiperCurrent +1 < this.topicData.length){
						 setTimeout(()=>{
						 	this.swiperCurrent = index +1
						 },500)
					 }
					
				}else{
					// 错误
					//当前img错误图标,正确答案改成正确下标
					this.topicData[index].options[indexa].icon_url = this.imgData[1]
					//遍历出正确答案下标
					const idx = this.topicData[index].options.findIndex(item=>item.select_id === correct_id[0])
					this.topicData[index].options[idx].icon_url = this.imgData[0]
					this.topicData[index].options[indexa].isCorrect = true
					this.topicData[index].options[idx].isCorrect = true
					// 存储答错题下标
					this.errorIndex.push(index)
					//取出正确答案顺序
					var sequenceData = this.sequence[idx]
					
				}
				//取出正确答案顺序更新数据
				this.topicData[index].correct_answer = [sequenceData]
				//已选择该题目
				this.topicData[index].answered = true
				// 进度条
				this.percent += 2
			},
			//多选题
			multipleChoice(index,indexa,select_id,correct_id,isCorrect,store_check_id){
				if(this.topicData[index].answered)return false
				if(isCorrect){
					const indexRemove = this.topicData[index].store_check_id.findIndex(item=>item === select_id)
					this.topicData[index].store_check_id.splice(indexRemove,1)
					this.topicData[index].options[indexa].isCorrect = false
				}else{
					this.topicData[index].store_check_id.push(select_id)
					this.topicData[index].options[indexa].isCorrect = true
				}
			},
			//多选题选中或取消选中
			multipTextStyle(isCorrect){
				if(isCorrect){
					return 'selected'
				}else{
					return ''
				}
			},
			//多选提交
			subMit(index,store_check_id,correct_id,options){
				
				const isSame = store_check_id.length === correct_id.length && store_check_id.every(item=>correct_id.includes(item))
				if(isSame){ //是否正确
					//保存正确题目下标
					this.correntIndex.push(index)
					//选择正确自动 进入下一题
					 if(this.swiperCurrent +1 < this.topicData.length){
						 setTimeout(()=>{
						 	this.swiperCurrent = index +1
						 },500)
					 }
				}else{
					this.errorIndex.push(index)
				}
				//正确答案展示
				const correctId = correct_id.map(value=>options.findIndex(item=>item.select_id === value))
				correctId.forEach(item=>{
					this.topicData[index].options[item].whetherSubmit = true
					this.topicData[index].options[item].icon_url = this.imgData[0]
					this.topicData[index].correct_answer.push(this.sequence[item])
				})
				//错误答案图标展示
				options.forEach((item,index)=>{
					if(!correct_id.includes(item.select_id)){
						this.errorId.push(index)
					}
				})
				if(this.errorId.length > 0){
					this.errorId.forEach(item=>{
						this.topicData[index].options[item].whetherSubmit = true
						this.topicData[index].options[item].icon_url = this.imgData[1]
					})
				}
				//已选择该题目
				this.topicData[index].answered = true
				// 进度条
				this.percent += 2
			},
			//滑动触发
			changeCurrent(event){
				console.log();
				this.currentOrder = event.detail.current +1
				
			},
			
			
			//错题正确题顺序加上样式
			getTestStyle(index){
				if(this.correntIndex.includes(index)){//选择正确的题
					return 'yes-text'
				}else if(this.errorIndex.includes(index)){//选择错误确的题
					return 'no-text'
				}else{
					return ''
				}
			},
			//点击题目序号滚动题目
			numericalOrder(index){
				this.swiperCurrent = index
				this.currentOrder= index +1
				this.showPopup = false
			},
			//每秒更新倒计时
			countdownStarts(){
				this.state.countdownInterval = setInterval(()=>{
					this.state.countdown--
					this.state.formattedTime= this.formatTime(this.state.countdown)
					if(this.state.countdown <= 0){
						clearInterval(this.state.countdownInterval)
						//倒计时结束自动交卷
						wx.showModal({
							title:'考试超时,即将自动交卷',
							icon:'none',
							duration:3000,
							mask:true
						})
					}
				},1000)
			}
			,
			//计算出分钟和秒
			formatTime(seconds){
				const mins = Math.floor(seconds /60)
				const secs = seconds %60
				return `${mins.toString().padStart(2,'0')}:${secs.toString().padStart(2,'0')}`
			}
			
			
		},
		
		
	}
</script>

<style>
	@import url("@/style.css");
	.selected{
		background-color: #54bf66;
		color: #ffffff;
		
	}
	.anaylze{
		margin: 8px;
	}
	.yes-text{
		background-color: #5dbf84 !important;
		color: #ffffff;
	}
	.no-text{
		background-color: red !important;
		color: #ffffff;
	}
	.analyze-correct text{
	}
</style>