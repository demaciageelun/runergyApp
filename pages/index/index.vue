<template>
	<view>
		<view class="uni-margin-wrap">
			<swiper class="swiper" circular :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval"
				:duration="duration">
				<swiper-item v-for="(item,i) in swiperList" :key="i">
					<navigator class="swiper-item" :url="'/subpkg/news_details/news_details?news_id=' +item.id">
						<image :src="item.url"></image>
					</navigator>
				</swiper-item>
			</swiper>
		</view>
		<view class="grid-container">
			<uni-grid :column="3" :showBorder="false" @change="navToDetail" square>
				<uni-grid-item v-for="(gridItem, index) in gridItemList" :index="index" :key="index">
					<view class="grid-item-box">
						<uni-icons :type="gridItem.icon" size="30"></uni-icons>
						<text class="text">
							{{gridItem.title}}
						</text>
					</view>
				</uni-grid-item>
			</uni-grid>
		</view>
	</view>
</template>

<script>
	export default {

		onLoad(options) {
			// 打开页面则校验身份
			wx.qy.login({
				success:function(res) {
					console.log(res);
				}
			})
			this.getUserInfo()
		},
		data() {
			return {
				code: '2010009598',
				background: ['color1', 'color2', 'color3'],
				indicatorDots: true,
				autoplay: true,
				interval: 2000,
				duration: 500,
				swiperList: [{
					'url': '/static/ssc.jpg'
				}, {
					'url': '/static/ssc.jpg'
				}],
				gridItemList: [{
					'title': '工资查询',
					'icon': 'map-pin-ellipse',
					'url': '/subpkg/salaryEntryPassword/salaryEntryPassword'
				}, {
					'title': '考勤查询',
					'icon': 'shop-filled',
					'url': '/subpkg/attendance/attendance'
				}, {
					'title': '协议签署',
					'icon': 'fire',
					'url': ''
				}, {
					'title': '入职办理',
					'icon': 'person',
					'url': '/subpkg/entryPersonInfo/entryPersonInfo'
				}, {
					'title': '我的信息',
					'icon': 'calendar',
					'url': '/subpkg/myInfo/myInfo'
				}, {
					'title': '我的档案',
					'icon': 'camera',
					'url': '/subpkg/myProfile/myProfile'
				}, {
					'title': '员工手册',
					'icon': 'home',
					'url': ''
				}, {
					'title': '社保确认',
					'icon': 'shop',
					'url': ''
				}]
			};
		},
		methods: {
			navToDetail(e) {
				if (this.code === '' && this.gridItemList[e.detail.index].title !== '入职办理') {
					uni.showToast({
						title: '请先办理入职',
						duration: 2000,
						icon:'error'
					});
				} else {
					var urls = this.gridItemList[e.detail.index].url
					uni.navigateTo({
						url: urls
					})
				}
			},
			getUserInfo() {
				console.log(123);
				uni.setStorageSync("userInfo", JSON.stringify({
					'code': '2010009598'
				}))
				this.code = '2010009598'
			}
		}
	}
</script>

<style lang="scss">
	page {
		background-color: #f5f5f5;
	}
	.uni-margin-wrap {
		width: 690rpx;
		width: 100%;
	}

	.swiper {
		height: 350rpx;
	}

	.swiper-item,
	image {
		width: 100%;
		height: 100%;
	}

	.grid-container {
		width: 100%;
		height: 500rpx;

		.grid-item-box {
			display: flex;
			flex: 1;
			flex-wrap: wrap;
			flex-direction: column;
			width: 100%;
			align-items: center;
			justify-content: center;
		}
	}
</style>