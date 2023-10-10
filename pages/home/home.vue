<template>
	<view>
		<view class="container">
			<view class="title">
				<image :src="heardPicUrl" class="logo"></image>
				<view class="person-info">
					<text class="userName">周为</text>
					<text class="department">信息技术部 | IT主管</text>
				</view>
				<uni-icons type="forward" size="24"></uni-icons>
			</view>
			<view class="message-container">
				<view class="message-list" v-for="(messageItem, index) in messageList" :index="index" :key="index">
					<view class="message-list-left">
						<uni-icons :type="messageItem.icon" size="18"></uni-icons>
						<text>{{messageItem.title}}</text>
					</view>
					<uni-icons type="forward" size="18"></uni-icons>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		onShow() {
			uni.setTabBarBadge({ //显示数字  
				index: 1, //tabbar下标
				text: this.messageList.length.toString() //数字
			})

		},
		data() {
			return {
				heardPicUrl: '/static/face.jpg',
				messageList: [{
						'icon': 'wallet',
						'title': '您2023年08月薪资已发放',
						'type': 'salary',
						'id': 1
					},
					{
						'icon': 'camera-filled',
						'title': '您的身份证有效期已过，请重新上传',
						'type': 'personInfo',
						'id': 2
					}, {
						'icon': 'wallet',
						'title': '您2023年08月薪资已发放',
						'type': 'salary',
						'id': 1
					},
					{
						'icon': 'camera-filled',
						'title': '您的身份证有效期已过，请重新上传',
						'type': 'personInfo',
						'id': 2
					}, {
						'icon': 'wallet',
						'title': '您2023年08月薪资已发放',
						'type': 'salary',
						'id': 1
					},
					{
						'icon': 'camera-filled',
						'title': '您的身份证有效期已过，请重新上传',
						'type': 'personInfo',
						'id': 2
					}, {
						'icon': 'wallet',
						'title': '您2023年08月薪资已发放',
						'type': 'salary',
						'id': 1
					},
					{
						'icon': 'camera-filled',
						'title': '您的身份证有效期已过，请重新上传',
						'type': 'personInfo',
						'id': 2
					}, {
						'icon': 'wallet',
						'title': '您2023年08月薪资已发放',
						'type': 'salary',
						'id': 1
					},
					{
						'icon': 'camera-filled',
						'title': '您的身份证有效期已过，请重新上传',
						'type': 'personInfo',
						'id': 2
					}, {
						'icon': 'wallet',
						'title': '您2023年08月薪资已发放',
						'type': 'salary',
						'id': 1
					},
					{
						'icon': 'camera-filled',
						'title': '您的身份证有效期已过，请重新上传',
						'type': 'personInfo',
						'id': 2
					}
				]
			};
		}
	}
</script>

<style lang="scss">
	page {
		background-color: #f5f5f5;
	}

	.container {
		width: 100%;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;

		.title {
			border-radius: 5px;
			width: 94%;
			height: 100px;
			background-color: #fff;
			margin: 10px 0px 10px 0px;
			display: flex;
			flex-direction: row;
			justify-content: space-around;
			align-items: center;

			.logo {
				width: 75px;
				height: 75px;
				border-radius: 50px;
			}

			.person-info {
				display: flex;
				flex-direction: column;
				justify-content: center;
				align-items: flex-start;

				.userName {
					font-weight: 700;
					margin-bottom: 10px;
				}

				.department {
					color: #C2C1C1;
				}
			}
		}

		.message-container {
			width: 94%;
			background-color: #fff;
			border-radius: 5px;

			.message-list {
				width: 100%;
				height: 50px;
				display: flex;
				flex-direction: row;
				justify-content: space-evenly;
				align-items: center;
				border: 1px solid #f5f5f5;

				.message-list-left {
					width: 90%;

					.uni-icons {
						margin-right: 10px;
					}

					text {
						font-size: 14px;
						color: #404040;
					}
				}
			}
		}
	}
</style>