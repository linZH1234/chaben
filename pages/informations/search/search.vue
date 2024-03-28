<template>
	<view>
		<view class="s_mian">
			<view class="bg-w">
				<input type="text" class="text-muted" v-model="searchKeyword" @input="search"  placeholder="请输入关键字" style="position: relative;">
				<image src="/static/images/common/search.png" style="display: flex; height: 45rpx;width: 45rpx; position: absolute;right: 55px;"  mode="aspectFill"></image>
				<view class="sous" style="width: 80rpx; font-size: 17px; font-weight: bold;" @click="search">
					搜索
				</view>
			</view>
			<view v-if="!searchKeyword" class="hot">
				<view class="hot_s">热门搜索</view>
				<view class="hot_s_h">
					<view v-for="(item,index) in hotwords" :key="index" class="hot_search" @click="hot(item)">
						{{item}}
					</view>
				</view>
			</view>
			<view v-else class="search_info">
				<view v-for="(item,index) in searchResults" :key="index">
					<view class="search_main">
					<view class="search_head">
						<view class="div1"><image :src="item.picture"></image></view>
						<view class="div2" style="margin-right: 55px;">{{item.name}}</view>
						<view class="div3">{{item.major}}</view>
					</view>
					<view class="div4"><view class="sp">专业课</view>{{item.考试科目}}</view>
					<view class="div5"><view class="sp">学费</view>{{item.学费}} </view>
					<view class="div5"><view class="sp">住宿费</view>{{item.住宿费}} </view>
					<view class="div5"><view class="sp"> 允许报考专科专业</view>{{item.允许报考的专科专业}}  </view>
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
			  searchKeyword: "", // 搜索关键词
			  searchResults: [],
				hotwords:[
					"计算机科学与技术","汉语言文学","会计","工商","数字媒体技术","数字媒体艺术"
				],
			}
		},
		onLoad: function (option) { //option为object类型，会序列化上个页面传递的参数
			this.searchKeyword = option.name;
			this.search()
		},
		 methods: {
		     async search() {
		       // 调用云函数进行搜索
		       const res = await uniCloud.callFunction({
		         name: "cloudfunction",
		         data: {
		           keyword: this.searchKeyword
		         }
		       });
			    this.searchResults = res.result.data;
		     },
			 hot(item){
				this.searchKeyword = item;
				this.search()
			 }
		   }
	}
</script>

<style>
.sp{
	 width: 80px;
	 margin: 0 5px 0 5px;
}
.div1 image{
	height: 24px;
	width: 24px;
}
.div4{
	display: flex;
	align-items: center;
	height: 60px;
	
}
.div4 span{
	width: 90px;
}
.div5{
	display: flex;
	height: 45px;
}
.search_info{
	background-color: white;
}
.search_main{
	margin-left: 9px;
	margin-top: 15px;
	padding-bottom: 30px;
	height: 250px;
	width: 95%;
	box-shadow: 0 0 1px rgb(0,153,184) inset,0 0 1px rgb(0,153,184);
	background-color: white;
}
.search_head{
	display: flex;
	justify-content: space-around;
	align-items: center;
	height: 50px;
	width: 90%;
	margin: 0 16px 0 16px;
	border-bottom: 1px solid #bbbeb8;
	
}
.s_main{
	display: flex;
	align-items: center;
}
input::-webkit-input-placeholder{
	left: 0.8rem;
}
.bg-w{
	padding-top: 2px;
	height: 100rpx;
	
	border-radius: 50rpx;
	display: flex;
	align-items: center;
}
.text-muted{
	margin-left: 15px;
	padding-left: 10px;
	width: 85%;
	height: 30px;
	font-size: 14px; 
	 border-radius: 10px;
	 background-color: white;
}
.sous{
	margin-left: 10px;
}
.hot{
	display: flex;
	flex-direction: column;
	
	
}
.hot_s{
	height: 35px;
	margin-top: 30px;
	margin-left: 15px;
	font-size: 16px;
	font-weight: bold;
}
.hot_s_h{
	display: flex;
	flex-wrap: wrap;
}
.hot_search{
	display: flex;
	justify-content: center;
	padding: 10rpx;
	border-radius: 2rpx;
	height: 50rpx;
	font-size: 14px;
	margin: 10px;
	background-color: white;
}
</style>
