<template>
	<view>
		<view class="box-container">
			<uni-section class="mb-10" title="常用功能" sub-title=""></uni-section>
			<view class="grid-container">
				<uni-grid :column="3" :showBorder="false" @change="navToDetail">
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
		<view class="box-container">
			<uni-section class="mb-10" title="员工服务" sub-title=""></uni-section>
			<view class="grid-container">
				<uni-grid :column="3" :showBorder="false" @change="navToDetailEmployeeServe">
					<uni-grid-item v-for="(gridItem, index) in employeeServeList" :index="index" :key="index">
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
		<view class="box-container">
			<uni-section class="mb-10" title="考勤管理" sub-title=""></uni-section>
			<view class="grid-container">
				<uni-grid :column="3" :showBorder="false" @change="navToDetail">
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
		<view class="box-container">
			<uni-section class="mb-10" title="薪酬绩效" sub-title=""></uni-section>
			<view class="grid-container">
				<uni-grid :column="3" :showBorder="false">
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
	</view>
</template>

<script>
	export default {
		data() {
			return {
				gridItemList: [{
					'title': 'SSC',
					'icon': 'map-pin-ellipse',
					'url': '/subpkg/ssc/ssc'
				}, {
					'title': 'COE',
					'icon': 'shop-filled',
					'url': ''
				}, {
					'title': '工资查询',
					'icon': 'fire',
					'url': ''
				}, {
					'title': '内部推荐',
					'icon': 'person',
					'url': ''
				}, {
					'title': '考勤查询',
					'icon': 'calendar',
					'url': ''
				}],
				employeeServeList: [{
					'title': '协议签署',
					'icon': 'map-pin-ellipse',
					'url': ''
				}, {
					'title': '入职办理',
					'icon': 'shop-filled',
					'url': ''
				}, {
					'title': '我的信息',
					'icon': 'fire',
					'url': '/subpkg/myInfo/myInfo'
				}, {
					'title': '我的档案',
					'icon': 'person',
					'url': '/subpkg/myProfile/myProfile'
				}, {
					'title': '员工手册',
					'icon': 'calendar',
					'url': ''
				}, {
					'title': '社保确认',
					'icon': 'calendar',
					'url': ''
				}]
			};
		},
		methods: {
			navToDetailEmployeeServe(e) {
				console.log(e);
				var urls = this.employeeServeList[e.detail.index].url
				uni.navigateTo({
					url: urls
				})
			}
		}
	}
</script>

<style lang="scss">
	.box-container {
		width: 100%;
		margin-bottom: 20px;

		.grid-container {
			width: 100%;

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
	}
</style>