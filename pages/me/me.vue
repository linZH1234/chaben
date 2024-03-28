<template>
	<!-- 引入组件库 -->

	<view class="">
	  <!-- 顶部个人信息 -->
	  <view class="bg-white">
	    <view class="flex padding">
	      <view class="padding-lr-xs">
			  <view class="user-login"  @click="login">
			  	<view class="cu-avatar lg round">
			  		<img style="width: 50px;height: 50px; border-radius: 50%;" :src="avatarUrl"/>
			  	</view>
				<text style="padding-left: 10px;">{{nickName}}</text>
				<view class="padding-xs text-xl text-black">
					
				<view >
					<!-- 普通弹窗 -->
<!-- 					<uni-popup v-show="show1" ref="popup" background-color="#fff" @change="change">
							<view class="popup-content" :class="{ 'popup-height': type === 'left' || type === 'right' }">
								<view class="get_user">
								    <button  open-type="chooseAvatar" bind:chooseavatar="onChooseAvatar" >
										<image wx:if="{{customerLevel.value}}" class="iconLevel" :src="avatarUrl" mode="" />
									</button>
									<input bindinput='getInputValue' name='value' type='nickname' @blur="onNickName" style="display: inline-block;" placeholder='请输入昵称'  >
								</view>
							</view>
					</uni-popup> -->

				</view>
				 
				</view>
			  </view>
	      </view>
	      
	    </view>
	  </view>
	  <!-- 基本数据 -->
	  <view class="cu-list grid col-4 no-border padding-lr-xs radius-lg-bottom">
	    <view class="cu-item">
	      <view class="text-black text-bold text-xxl">
	        0
	      </view>
	      <text>我的题库</text>
	    </view>
	    <view class="cu-item">
	      <view class="text-black text-bold text-xxl">
	        0
	      </view>
	      <text>联系历史</text>
	    </view>
	    <view class="cu-item">
	      <view class="text-black text-bold text-xxl">
	        0
	      </view>
	      <text>我的资料</text>
	    </view>
	    <view class="cu-item" @click="sign">
	      <view class="text-black text-bold text-xxl">
	        0
	      </view>
	      <text>打卡</text>
	    </view>
	  </view>
	  <!-- 助力/推荐/邀请 -->
	  <view class="margin-top-sm padding-lr-xs">
	    <view class="bg-brown light radius-lg shadow-blur">
	      <view class="flex padding-tb-sm padding-lr-sm justify-between">
<!-- 	        <view class="padding-xs">
	          <view>9.9元开通超级会员最高可省￥40</view>
	        </view>
	        <view class="">
	          <view class="cu-btn round bg-black">开通会员</view>
	        </view> -->
	      </view>
	    </view>
	  </view>
	  <!-- 常用功能 -->
	  <view class="cu-bar margin-lr-xs margin-top-sm grid col-4 no-border bg-white radius-lg-top">
	    <view class="action">
	      <text class="text-xl text-black">我的资料	</text>
	    </view>
	    <view class="action">
	      <text class="text-lg">全部资料<text class="cuIcon-right"></text></text>
	    </view>
	  </view>
	  <view class="cu-list grid col-4 no-border text-black margin-lr-xs padding-bottom radius-lg-bottom">
	    <view class="cu-item" v-for="(item,index) in iconList" :key="index" :bindtap="item.bindtap">
	      <view :class="['cuIcon-'+item.icon,'text-'+item.color,'text-shadow']" style="font-size: 56rpx;">
	        <view class="cu-tag badge" v-if="item.badge!=0">
	          <block v-if="item.badge!=1">{{item.badge>99?"99+":item.badge}}</block>
	        </view>
	      </view>
	      <text>{{item.name}}</text>
	    </view>
	  </view>
	
	  <view class="margin-top-sm padding-lr-xs">
	    <view class="bg-white light radius-lg shadow-blur">
	      <view class="flex padding-tb-sm padding-lr-sm justify-between">
	        <view class="padding-xs">
	          <view class="text-xl text-black">惊喜连连</view>
	          <view class="padding-top-xs">开通<text class="text-red text-bold"> 6.6折 </text><text class="cuIcon-roundrightfill text-red"></text></view>
	        </view>
	        <view class="">
	          <view class="cu-btn round bg-gradual-pinknew margin-top-sm">6折优惠</view>
	        </view>
	      </view>
	    </view>
	  </view>
	  <!-- 其他功能 -->
	  <view class="cu-bar margin-lr-xs margin-top grid col-4 no-border bg-white radius-lg-top">
	    <view class="action">
	      <text class="text-xl">其他功能</text>
	    </view>
	  </view>
	  <view class="cu-list grid col-4 no-border text-black margin-lr-sm padding-bottom radius-lg-bottom">
	    <view class="cu-item" v-for="(item,index) in iconOtherList" :key="index" :bindtap="item.bindtap">
	      <view :class="['cuIcon-'+item.icon,'text-'+item.color,'text-shadow']" style="font-size: 56rpx;">
	        <view class="cu-tag badge" v-if="item.badge!=0">
	          <block v-if="item.badge!=1">{{item.badge>99?"99+":item.badge}}</block>
	        </view>
	      </view>
	      <text>{{item.name}}</text>
	    </view>
	  </view>
	
	</view>
</template>

<script>
	export default {
		data() {
			return {
				openid:"",
				nickName:getApp().globalData.nickName,
				avatarUrl:'https://pic1.zhimg.com/50/v2-6afa72220d29f045c15217aa6b275808_hd.jpg?source=1940ef5c',
				type:'button',
				 iconList: [{
				      icon: 'moneybagfill',
				      color: 'blue',
				      badge: 0,
				      name: '我的钱包'
				    }, {
				      icon: 'presentfill',
				      color: 'red',
				      badge: 0,
				      name: '我的题库',
				      bindtap: "bindZan"
				    }, {
				      icon: 'formfill',
				      color: 'purple',
				      badge: 0,
				      name: '我的打卡',
				      bindtap: "showResource"
				    }, {
				      icon: 'shopfill',
				      color: 'green',
				      badge: 0,
				      name: '我的积分',
				      bindtap: "bindPoint"
				    }],
				    iconOtherList: [{
				      icon: 'location',
				      color: 'blue',
				      badge: 0,
				      name: '地址管理'
				    }, {
				      icon: 'service',
				      color: 'blue',
				      badge: 0,
				      name: '电话客服',
				      bindtap: "bindZan"
				    }, {
				      icon: 'mark',
				      color: 'blue',
				      badge: 0,
				      name: '在线客服',
				      bindtap: "showResource"
				    }, {
				      icon: 'mail',
				      color: 'blue',
				      badge: 0,
				      name: '投诉',
				      bindtap: "bindCollect"
				    }, {
				      icon: 'settings',
				      color: 'blue',
				      badge: 0,
				      name: '设置',
				      bindtap: "bindZan"
				    }]
			}

		},
		// onShow() {
		//     this.nickName = getApp().globalData.nickName;
		// 	this.avatarUrl = getApp().globalData.avatarUrl;
		//     console.log(this.nickName); // 输出：'Hello, World!'
		//   },
		onChooseAvatar(e) {

			console.log(e.detail.avatarUrl)
				this.avatarUrl = e.detail.avatarUrl
		  },
		methods: {
		// onshow(){
		// 	console.log(getApp().globalData.nickName+"111");
		// 	console.log("开始");
			
		// },
			sign(){
				wx.redirectTo({
					url:'/pages/sign/index'
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
			toggle(type) {
				this.type = type
				// open 方法传入参数 等同在 uni-popup 组件上绑定 type属性
				this.$refs.popup.open(type);
			},
			login(){
				wx.login({
					success: res => {
						if (res.code) {
						  let URL='https://api.weixin.qq.com/sns/jscode2session?appid=wx115fcf2d47d1cf88&secret=e3e459f0afd65a113e841ed12178edab&js_code='+res.code+'&grant_type=authorization_code'
						  wx.request({
							url: URL , 
							 success:function(res){ 
								 this.openid = res.data.openid
								 console.log(this.openid)
								 wx.setStorageSync('openid',this.openid);
							}.bind(this),
							
						  })
						}  
				} })
				uni.getUserProfile({
					desc: '你的授权信息',
					success: (res) => {
						this.nickName = res.userInfo.nickName
						this.avatarUrl = res.userInfo.avatarUrl
						console.log(res)
					  // 将信息存到 vuex 中
					  this.updateUserInfo(res.userInfo)
					  // this.getToken(res)
					},
					fail: (res) => {
					  return uni.$showMsg('您取消了登录授权')
					}
				  })//在methods节点中定义login
			},
			async updateUserInfo(user){
			   const res = await uniCloud.callFunction({
				 name: "userupdate",
				 data: {
				   avatarUrl: user.avatarUrl,
				   nickName:user.nickName,
				   openid:this.openid
				 }
			   });
			}
		
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
	}
	.get_user input{
		margin-top: 10rpx;
		border: 1px solid gray;
		border-radius: 10rpx;
		display: inline-block;
	}
	.getpop{
		width: 100%;
		position: fixed;
		left: 0;
		bottom: 0;
	}
	@mixin flex {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: row;
	}

	@mixin height {
		/* #ifndef APP-NVUE */
		height: 100%;
		/* #endif */
		/* #ifdef APP-NVUE */
		flex: 1;
		/* #endif */
	}

	.box {
		@include flex;
	}

	.button {
		@include flex;
		align-items: center;
		justify-content: center;
		flex: 1;
		height: 35px;
		margin: 0 5px;
		border-radius: 5px;
	}

	.example-body {
		background-color: #fff;
		padding: 10px 0;
	}

	.button-text {
		color: #fff;
		font-size: 12px;
		width: 20px;
		justify-content: center;
	}

	.popup-content {
		@include flex;
		flex-direction: column;
		padding: 15px;
		height: 200px;
		background-color: #fff;
	}

	.popup-height {
		@include height;
		width: 400px;
	}

	.text {
		font-size: 12px;
		color: #333;
	}

	.popup-success {
		color: #fff;
		background-color: #e1f3d8;
	}

	.popup-warn {
		color: #fff;
		background-color: #faecd8;
	}

	.popup-error {
		color: #fff;
		background-color: #fde2e2;
	}

	.popup-info {
		color: #fff;
		background-color: #f2f6fc;
	}

	.success-text {
		color: #09bb07;
	}

	.warn-text {
		color: #e6a23c;
	}

	.error-text {
		color: #f56c6c;
	}

	.info-text {
		color: #909399;
	}

	.dialog,
	.share {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: column;
	}

	.dialog-box {
		padding: 10px;
	}

	.dialog .button,
	.share .button {
		/* #ifndef APP-NVUE */
		width: 100%;
		/* #endif */
		margin: 0;
		margin-top: 10px;
		padding: 3px 0;
		flex: 1;
	}

	.dialog-text {
		font-size: 14px;
		color: #333;
	}
</style>

