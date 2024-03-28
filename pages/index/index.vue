<template>

	<view id="index">
		<!-- 顶部导航 -->
		<u-navbar v-if="navBarShowTag">
			<view class="tabs-box">
				<view class="one-nav" :class="currentSwiperIndex === 0 ? 'nav-actived' : '' " @tap="swiperChange(0)">推荐</view>

				<view class="one-nav" :class="currentSwiperIndex === 1 ? 'nav-actived' : '' " @tap="swiperChange(1)">资讯</view>
			</view>
		</u-navbar>

		<!-- 页面 header 相关部分 -->
		<view class="header-box">
			<!-- 顶部广告位轮播图 -->
			<swiper class="swiper" circular :indicator-dots="false" :autoplay="true" :interval="2500"
							:duration="500">
					<swiper-item>
						<view class="swiper-item uni-bg-red"><img src="@/static/a.jpg" alt=""></view>
					</swiper-item>
					<swiper-item>
						<view class="swiper-item uni-bg-green"><img src="@/static/b.jpg" alt=""></view>
					</swiper-item>
					<swiper-item>
						<view class="swiper-item uni-bg-blue"><img src="@/static/c.jpg" alt=""></view>
					</swiper-item>
				</swiper>
			<!-- 遮罩使用弧形框 -->
			<image class="crile" src="@/static/crile.png" mode="aspectFill" />
			<!-- 两个选项按钮 -->
			<view class="card-header">
				<view class="card-one card-left" @tap="gotoTab('/pages/test/test')">
					<image class="img" src="@/static/coffee.png" mode="aspectFill" />
					<view class="iright">
						<view class="title">在线答题</view>
					</view>
				</view>
				<view class="card-one card-right" @click="gotopage('/pages/sign/index')">
					<image class="img" src="@/static/ran.png" mode="aspectFill" />
					<view class="iright">
						<view class="title">每日签到</view>
					</view>
				</view>
			</view>
			
			<!-- Tab 选项卡 -->
			<view class="tabs-box">
				<view class="one-nav" :class="currentSwiperIndex === 0 ? 'nav-actived' : '' " @tap="swiperChange(0)">推荐</view>
				<view class="one-nav" :class="currentSwiperIndex === 1 ? 'nav-actived' : '' " @tap="swiperChange(1)">资讯</view>
			</view>
			
			
			<view>
				
				<navigator url="/subpages/chat/chat">客服聊天</navigator>
			</view>
		</view>
		<swiper class="swiper-box" :style=" 'height:'+ swiperSliderHeight " :current="currentSwiperIndex" @animationfinish="swiperSlider">
			<!-- 推荐动态实现 -->
			<swiper-item class="swiper-item">
				<view class="page-item sns-now">
					<view class="feeds-box">
							<template>
								<view class="feed-one">
									<navigator open-type="navigate" url="/pages/webview/webview?url=http://mp.weixin.qq.com/s/YGk8s3523hzIjQexgX8mLQ">
										<image class="feed-img" src="@/static/a.jpg" />
										<view class="u-line-2 feed-title">2024年专插本网课开课通知</view>
										<view class="feed-info">
											<view class="iview">
												<image class="avatar" src="@/static/c.jpg" />
												<text class="name u-line-1">qqqqqqqqqqqqqqqqqqqqqqq</text>
											</view>
											<view class="iview">
												<view class="ilike">
													<image src="@/static/love.png" class="micon" />
													<text class="love-count">0</text>
												</view>
											</view>
										</view>
									</navigator>
								</view>
								<view class="feed-one" style="float: right;">
									<navigator open-type="navigate" url="/pages/webview/webview?url=http://mp.weixin.qq.com/s/YGk8s3523hzIjQexgX8mLQ">
										<image class="feed-img" src="@/static/b.jpg" />
										<view class="u-line-2 feed-title">2024年专插本网课开课通知</view>
										<view class="feed-info">
											<view class="iview">
												<image class="avatar" src="@/static/c.jpg" />
												<text class="name u-line-1">qqqqqqqqqqqqqqqqqqqqqqq</text>
											</view>
											<view class="iview">
												<view class="ilike">
													<image src="@/static/love.png" class="micon" />
													<text class="love-count">0</text>
												</view>
											</view>
										</view>
									</navigator>
								</view>
								<view class="feed-one" style="float: right;">
									<navigator open-type="navigate" url="/pages/webview/webview?url=https://mp.weixin.qq.com/s/YGk8s3523hzIjQexgX8mLQ">
										<image class="feed-img" src="@/static/c.jpg" />
										<view class="u-line-2 feed-title">2024年专插本网课开课通知</view>
										<view class="feed-info">
											<view class="iview">
												<image class="avatar" src="@/static/a.jpg" />
												<text class="name u-line-1">qqqqqqqqqqqqqqqqqqqqqqq</text>
											</view>
											<view class="iview">
												<view class="ilike">
													<image src="@/static/love.png" class="micon" />
													<text class="love-count">0</text>
												</view>
											</view>
										</view>
									</navigator>
								</view>
								<view class="feed-one" style="float: right;">
									<navigator open-type="navigate" url="">
										<image class="feed-img" src="@/static/a.jpg" />
										<view class="u-line-2 feed-title">2024年专插本网课开课通知</view>
										<view class="feed-info">
											<view class="iview">
												<image class="avatar" src="@/static/b.jpg" />
												<text class="name u-line-1">qqqqqqqqqqqqqqqqqqqqqqq</text>
											</view>
											<view class="iview">
												<view class="ilike">
													<image src="@/static/love.png" class="micon" />
													<text class="love-count">0</text>
												</view>
											</view>
										</view>
									</navigator>
								</view>
								
							</template>
					</view>
				</view>
			</swiper-item>
			<!-- 资讯列表实现 -->
			<swiper-item class="swiper-item sns-news">
				<view >
					<navigator class="one-new" open-type="navigate" url="/pages/webview/webview?url=https://mp.weixin.qq.com/s/YGk8s3523hzIjQexgX8mLQ">
						<view class="left">
							<view class="title">2024年专插本报名时间确认
							</view>
							
						</view>
						
						<view class="right">
							<image class="pic" src="@/static/a.jpg" />
						</view>
					</navigator>
					<navigator class="one-new" open-type="navigate" url="/pages/webview/webview?url=https://mp.weixin.qq.com/s/YGk8s3523hzIjQexgX8mLQ">
						<view class="left">
							<view class="title">2024年专插本报名时间确认</view>
							
						</view>
						<view class="right">
							<image class="pic" src="@/static/b.jpg" />
						</view>
					</navigator>
					<navigator class="one-new" open-type="navigate" url="/pages/webview/webview?url=https://mp.weixin.qq.com/s/YGk8s3523hzIjQexgX8mLQ">
						<view class="left">
							<view class="title">2024年专插本报名时间确认</view>
						</view>
						<view class="right">
							<image class="pic" src="@/static/c.jpg" />
						</view>
					</navigator>
					<navigator class="one-new" open-type="navigate" url="">
						<view class="left">
							<view class="title">2024年专插本报名时间确认</view>
						</view>
						<view class="right">
							<image class="pic" src="@/static/c.jpg" />
						</view>
					</navigator>
				</view>
			</swiper-item>

		</swiper>
		
	</view>
</template>

<script>
	// 引入 个性化 瀑布流组件
	import WaterfallSns from '@/components/waterfall-sns/index.vue'
	import feedMixin from '@/mixins/todoFeed.js'
	export default {
		data(){
			return{
				
				// background: ['color1', 'color2', 'color3'],
				indicatorDots: true,
				autoplay: true,
				interval: 2000,
				duration: 500,
				// navBar 显示状态控制
				navBarShowTag: false,
				// 顶部 轮播图列表
				swiperAdList: [],
				// 动态列表数据
				feedsList: [],
				// 资讯列表数据
				newsList: [],
				// 当前 推荐 资讯 滑动位置
				currentSwiperIndex: 0,
				// 滑动页面轮播器的高度
				swiperSliderHeight: '500px',
				swiperSliderFeedsHeight: 0,
				swiperSliderNewsHeight: 0,
				// 记录滚动所在的位置
				oldFeedsScrollTop: 0,
				oldNewsScrollTop: 0

			}
		},
		components: {
			WaterfallSns
		},
		onShow(){
			console.log('Inded page show')
		},
		onLoad(){
		},
		onPullDownRefresh(){
			console.log('页面下拉刷新')
		},
		methods: {
			// 页面滑动左右分页的时候实现的效果
			swiperSlider(event) {
				this.currentSwiperIndex = event.detail.current
			},
			// 点击按钮实现切换效果
			swiperChange(index) {
					this.currentSwiperIndex = index;
				// 可选：如果需要，在切换选项卡时滚动到页面顶部
					uni.pageScrollTo({
					duration: 0,
					scrollTop: 0,
					});
	
			},
			//设置跳转方法
			gotopage(url){
				uni.navigateTo({
				  url: url
				})

			},
			gotoTab(url){
				uni.switchTab({
					url
				})
			},
			
			changeIndicatorDots(e) {
				this.indicatorDots = !this.indicatorDots
			},
			changeAutoplay(e) {
				this.autoplay = !this.autoplay
			},
			intervalChange(e) {
				this.interval = e.target.value
			},
			durationChange(e) {
				this.duration = e.target.value
			},
			
		}
	}
</script>

<style lang="scss" scoped>
	
#sns {
	background-color: #f1f1f1;
}

// 推荐、咨询 按钮样式
.tabs-box {
	display: flex;
	flex-direction: row;
	justify-content: center;
	width: 750upx;

	.one-nav {
		width: 120upx;
		color: #9B9B9B;
		font-size: 36upx;
		text-align: center;
		font-weight: blod;

		&.nav-actived {
			color: #0050FF;
		}
	}
}

.header-box {
	position: relative;
	left: 0;
	height: 500upx;
	background-color: #f1f1f1;
	z-index: 1;

	// 广告位轮播器相关样式
	.swiper {
		width: 750upx;
		height: 400upx;
		position: absolute;
		left: 0;
		top: 0;
		text-align: center;
		z-index: 1;

		.banner-swiper-img {
			width: 750upx;
			height: 400upx;
			box-shadow: 0 0 2px 0 rgb(188, 188, 188);
		}
	}

	.crile {
		width: 750upx;
		height: 50upx;
		position: absolute;
		left: 0;
		top: 355upx;
		z-index: 9;
	}

	// 新鲜事 活动墙 按钮样式
	.card-header {
		position: absolute;
		left: 0;
		top: 320upx;
		height: 160upx;
		z-index: 99;
		width: 710upx;
		margin-left: 20upx;
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
		justify-content: space-between;
		align-items: center;
		align-content: center;

		.card-one {
			width: 328upx;
			height: 96upx;
			border-radius: 49upx;
			background-color: #fff;
			margin: 0 10upx;
			box-shadow: 0 0 2px 0 rgb(188, 188, 188);
			display: flex;
			flex-direction: row;
			flex-wrap: wrap;
			justify-content: flex-start;
			align-items: center;
			align-content: center;

			.img {
				width: 44upx;
				height: 44upx;
				margin-left: 50upx;
			}

			.iright {
				margin-left: 30upx;
				text-align: left;
				color: #888;

				.title {
					font-size: 27upx;
					color: #001432;
				}

				.iview {
					display: flex;
					flex-direction: row;
					flex-wrap: wrap;
					justify-content: space-between;
					align-items: center;
					align-content: center;
					font-size: 20upx;
					margin-top: -5upx;
				}
			}
		}
	}

	// 推荐、咨询 按钮样式
	.tabs-box {
		width: 750upx;
		position: absolute;
		z-index: 1;
		left: 0;
		top: 480upx;
		display: flex;
		flex-direction: row;
		justify-content: center;

		.one-nav {
			height: 80upx;
			width: 110upx;
			color: #9B9B9B;
			font-size: 36upx;
			text-align: center;
			font-weight: blod;

			&.nav-actived {
				color: #0050FF;
			}
		}
	}
}

// 此刻 栏目样式\
.swiper-box {
	background-color: #f1f1f1;
	padding: 60upx 0 40upx;
}

.sns-now {

	// 动态相关瀑布流样式
	.feeds-box {
		display: flex;
		flex-wrap: wrap;
		width: 735upx;
		margin-left: 13upx;
		padding-bottom: 20upx;

		.feed-one {
			width: 358upx;
			
			margin-bottom: 12upx;
			margin-left: 8upx;
			background-color: #FFF;
			border-radius: 20upx;

			position: relative;

			.feed-img {
				width: 358upx;
				height: 300upx;
				border-radius: 10upx;
			}

			.feed-title {
				width: 350upx;
				margin-top: 15upx;
				margin-left: 10upx;
				font-size: 28upx;
				line-height: 40upx;
				color: #001432;
				text-align: left;
			}

			.feed-info {
				height: 50px;
				display: flex;
				flex-direction: row;
				flex-wrap: nowrap;
				justify-content: space-between;
				align-items: center;
				align-content: center;
				margin-top: 10upx;
				font-size: 20upx;
				color: #666;
				padding: 0 10upx 16upx;

				.iview {
					display: flex;
					flex-direction: row;
					flex-wrap: nowrap;
					justify-content: space-between;
					align-items: center;
					align-content: center;

					.ilike {
						display: flex;
						flex-direction: row;
						flex-wrap: nowrap;
						justify-content: space-between;
						align-items: center;
						align-content: center;
						height: 60upx;
						padding: 0 10upx;
						background-color: #FFFFFF;
					}
				}

				.avatar {
					margin-right: 10upx;
					height: 40upx;
					width: 40upx;
					border-radius: 50%;
					border: 1upx solid #eee;
				}

				.name {
					max-width: 120upx;
					color: #757474;
				}

				.micon {
					width: 32upx;
					height: 28upx;
				}

				.love-count {
					padding-left: 10upx;
					color: #757474;
				}
			}
		}
	}
}

// 轮播页面 资讯
.sns-news {
	background-color: #fff;
	width: 750upx;

	.one-new {
		width: 100%;
		height: 120px;
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding-bottom: 10px;
		border-bottom: 1px solid #f1f1f1;

		.left {
			.title {
				font-size: 30upx;
				line-height: 42upx;
				color: #001432;
			}

		}

		.right {
			width: 180upx;

		.pic {
			width: 170upx;
			height: 170upx;
			border-radius: 6upx;
		}
	}
	}
}
.uni-margin-wrap {
	width: 690rpx;
	width: 100%;
}
.swiper {
	height: 300rpx;
}
.swiper-item {
	display: block;
	height: 300rpx;
	line-height: 300rpx;
	text-align: center;
}
.swiper-list {
	margin-top: 40rpx;
	margin-bottom: 0;
}
.uni-common-mt {
	margin-top: 60rpx;
	position: relative;
}
.info {
	position: absolute;
	right: 20rpx;
}
.uni-padding-wrap {
	width: 550rpx;
	padding: 0 100rpx;
}
</style>
