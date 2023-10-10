<template>
	<view>
		<privacyPopup></privacyPopup>
		<view class="box-container">
			<view class="list-container" v-for="(fileItem, index) in fileTemplateList" :index="index" :key="index"
				@click="navigateTo(fileItem.id)">
				<view class="left-container">
					<view class="icon-container"><uni-icons :type="fileItem.icon" size="30"></uni-icons></view>
					<text class="title-container">{{fileItem.title}}</text>
				</view>
				<view class="status-container" :style='{backgroundColor:fileItem.bgColor,color:fileItem.fontColor}'>
					<text>{{fileItem.status}}</text></view>
			</view>
		</view>
	</view>
</template>

<script>
	import privacyPopup from '../../components/privacyPopup.vue';
	export default {
		components: {
			privacyPopup
		},
		data() {
			return {
				fileTemplateList: [{
					'title': '身份证	',
					'icon': 'calendar',
					'id': 1,
					'status': '缺失(必填项)',
					'bgColor': "#FFC0CB",
					'fontColor': '#CD0000'
				}, {
					'title': '毕业证	',
					'icon': 'fire',
					'id': 2,
					'status': '有效',
					'bgColor': "#87CEFA",
					'fontColor': '#12A0E8'
				}, {
					'title': '学位证	',
					'icon': 'medal',
					'id': 3,
					'status': '有效',
					'bgColor': "#87CEFA",
					'fontColor': '#12A0E8'
				}, {
					'title': '职称/技能证书',
					'icon': 'font',
					'id': 4,
					'status': '有效',
					'bgColor': "#87CEFA",
					'fontColor': '#12A0E8'
				}, {
					'title': '劳动合同',
					'icon': 'gift',
					'id': 5,
					'status': '有效',
					'bgColor': "#87CEFA",
					'fontColor': '#12A0E8'
				}, {
					'title': '保密协议',
					'icon': 'auth',
					'id': 6,
					'status': '暂无',
					'bgColor': "#EFEFEF",
					'fontColor': '#949494'
				}, {
					'title': '竞业限制',
					'icon': 'contact',
					'id': 7,
					'status': '暂无',
					'bgColor': "#EFEFEF",
					'fontColor': '#949494'
				}, {
					'title': '员工基本信息登记表',
					'icon': 'upload',
					'id': 8,
					'status': '暂无',
					'bgColor': "#EFEFEF",
					'fontColor': '#949494'
				}, {
					'title': '法律文书送达信息确认书',
					'icon': 'pyq',
					'id': 9,
					'status': '暂无',
					'bgColor': "#EFEFEF",
					'fontColor': '#949494'
				}, {
					'title': '重要事项告知书',
					'icon': 'map-pin-ellipse',
					'id': 10,
					'status': '暂无',
					'bgColor': "#EFEFEF",
					'fontColor': '#949494'
				}, {
					'title': '员工入职手续确认单',
					'icon': 'map-pin-ellipse',
					'id': 11,
					'status': '暂无',
					'bgColor': "#EFEFEF",
					'fontColor': '#949494'
				}, {
					'title': '离职证明/声明',
					'icon': 'map-pin-ellipse',
					'id': 12,
					'status': '暂无',
					'bgColor': "#EFEFEF",
					'fontColor': '#949494'
				}, {
					'title': '体检报告',
					'icon': 'map-pin-ellipse',
					'id': 13,
					'status': '暂无',
					'bgColor': "#EFEFEF",
					'fontColor': '#949494'
				}, {
					'title': '简历',
					'icon': 'map-pin-ellipse',
					'id': 14,
					'status': '暂无',
					'bgColor': "#EFEFEF",
					'fontColor': '#949494'
				}]
			};
		},
		methods: {
			navigateTo(val) {
				uni.navigateTo({
					url: '/subpkg/profileInfo/profileInfo?fileTypeId='+String(val)
				})
			}
		},
	}
</script>
<style lang="scss">
	page {
		background-color: #f5f5f5;
	}

	.box-container {
		width: 100%;
		display: flex;
		flex-direction: column;
		align-items: center;

		.list-container {
			width: 90%;
			height: 80px;
			border-radius: 10px;
			background-color: #fff;
			display: flex;
			flex-direction: row;
			justify-content: space-between;
			align-items: center;
			margin-bottom: 10px;

			.left-container {
				display: flex;
				flex-direction: row;
				align-items: center;
				justify-content: center;

				.icon-container {
					display: flex;
					flex-direction: column;
					align-items: center;
					justify-content: center;
					height: 50px;
					width: 50px;
					border-radius: 50px;
					background-color: #f5f5f5;
					margin-left: 10px;
				}

				.title-container {
					font-size: 16px;
					font-weight: 800;
					margin-left: 20px;
				}
			}

			.status-container {
				margin-right: 10px;
				height: 20px;
				font-size: 10px;
				font-weight: 400;
				border-radius: 7px;

				text {
					padding: 3px 10px 3px 10px;
					text-align: center;
					line-height: 20px;
				}
			}
		}
	}
</style>