<template>
	<view>
		<view @query="queryList" >
			<view slot="top">
				<view class="main-bg-color">
					<view class="w-100" style="width: 700rpx;">
						<view class="bg-white" @click.stop="search">
							<image src="/static/images/common/search.png" style="left: 5px; height: 45rpx;width: 45rpx;" mode="aspectFill">
							</image>
							<text class="text-muted" style="padding-left: 20px;font-size: 17px;">请输入学校或专业</text>
						</view>
					</view>
				</view>
				<view style="border-bottom: 1px solid gainsboro;background-color: white;height: 50px; margin-bottom: 6px;display: flex;align-items: center;"><text style="color: darkblue">推荐</text></view>
				<view v-for="(item,index) in dataList" :key="index" @click="" class="article" >
						<image class="art-img" :src=item.picture mode=""></image>
						<view class="art-name" @click="schinfor(item.name)">{{item.name}} </view>
						<image class="art-right" src="/static/images/common/return-right.png" mode=""></image>
					
				</view>
			</view>
			
		</view>
	</view>
</template>

<script>
	import information from '@/mockdata/information.json'
	export default {
		data() {	
			return {
				dataList:[]
			}
		},
		onLoad(){
			uniCloud.callFunction({
				name:"schoolfunction",
			}).then(res=>{
				this.dataList = res.result.data;
			})
		},
		methods: {
			schinfor(name1) {
				 uni.navigateTo({
				    url: '/pages/informations/search/search?name='+name1,
				  });
			 //  // 调用云函数进行搜索
			 //  const res = await uniCloud.callFunction({
			 //    name: "schinforfunction",
			 //    data: {
			 //      name: name1
			 //    },
				
			 //  });
			 //  console.log(res)
			 //  console.log(1)
			},
			init(){
				this.getAdvertList()
			},
			queryList(pageNo,pageSize){
				console.log("queryList",pageNo,pageSize)
				let that = this;
				
				this.$refs.paging.complete(this.dataList); 
			},
			getAdvertList(){
				let that = this;
				vk.callFunction({
					url:'client/schools/pub/getList',
					title:'',
					data:{},
					success(data){
						console.log("getAdvertList",data)
					}
				});
			},
			search(){
				uni.navigateTo({
					url:'/pages/informations/search/search'
				})
			},
			
		}
	}
</script>

<style>

.main-bg-color{
	height:120rpx;
	background-color: skyblue;
	display: flex;
	align-items: center;
	justify-content: center;
}
.bg-white{
	background-color: whitesmoke;
	height: 50rpx;
	border-radius: 50rpx;
	display: flex;
	align-items: center;
}
	
.article{
	
	background-color: white;
	border-bottom: 1px solid gainsboro;
	margin-bottom: 4px;
	display: flex;
	justify-content: space-between;
	align-items: center;
}
	.art-img{
		height: 27px;
		width: 27px;
		margin-left: 10px;
		
	}
	.art-name{
		margin-left: 10px;
		width:300px;
		display: flex;
		align-items: center;
		height: 90rpx;
		
	}
	.art-right{
		height: 17px;
		width: 17px;
	}
</style>
