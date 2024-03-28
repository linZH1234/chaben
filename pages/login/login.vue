<template>
	<view class="popup-content" :class="{ 'popup-height': type === 'left' || type === 'right' }">
		<view class="get_user">
			<button  open-type="chooseAvatar" bind:chooseavatar="onChooseAvatar" >
				<image :src="avatarUrl" mode="" />
			</button>
		</view>
		<view class="ninput">
		<span>昵称</span> <input class="minput" bindinput='getInputValue' name='value' type='nickname' @blur="onNickName" style="display: inline-block;" placeholder='请输入昵称'  >
		</view>
	</view>
	<view>
		<button @click="update">登录</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				nickName:'未登录',
				avatarUrl:'https://th.bing.com/th/id/OIP.xA5QX2crc3fR5d0DIH-oDQAAAA?w=183&h=183&c=7&r=0&o=5&pid=1.7',
				type:'button',
			}

		},
			
		onChooseAvatar(e) {

			console.log(e.detail.avatarUrl)
				this.avatarUrl = e.detail.avatarUrl
		  },
		methods: {
			update(){
				getApp().globalData.nickName= this.nickName
				getApp().globalData.avatarUrl= this.avatarUrl
				console.log(getApp().globalData.nickName)
				uni.switchTab({
						url:'/pages/me/me'
						
				    })

			},
		  onNickName(e) {
				this.nickName = e.detail.value
			},
			getInputValue(e){
			  console.log(e.detail)
			  this.nickName = e.detail.nickName
			},
			change(e) {
				console.log('当前模式：' + e.type + ',状态：' + e.show);
			},
			
		
		}
	}
</script>

<style lang="scss">
	.get_user{
		margin-top: 50rpx;
		margin-bottom: 80rpx;
		display: flex;
		flex-direction: column;
		align-items: center;
	}
	.get_user image{
		width: 100rpx;
		height: 100rpx;
		border-radius: 50%;
		top: 10px;
	}
	.ninput{
		margin-top: 50rpx;
		height: 50px;
		width: 100%;
		border-bottom: 1px solid gray;
		border-top: 1px solid gray;
	}
	span{
		margin-top: 10px;
		font-size: 15px;
	}
	.minput{
		padding-left: 100px;
		margin-top: 10px;
	}
	.popup-content {
		flex-direction: column;
		padding: 15px;
		height: 200px;
		background-color: #fff;
	}

</style>

