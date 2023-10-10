<template>
	<view class="container">

		<view class="box-container">
			<uni-section class="mb-10" :title="fileType[fileTypeId]" sub-title="" titleFontSize="20px"></uni-section>
			<uni-swipe-action>
				<!-- 基础用法 -->
				<uni-swipe-action-item :right-options="options" :left-options="options" @click="onClick"
					@change="swipeChange" v-for="(fileItem, index) in fileList" :index="index" :key="index">
					<view class="list-container" @click="dialogToggle(fileItem.url)">
						<view class="image-content">
							<image style="width: 50px; height: 50px" :src="fileItem.pic"></image>
						</view>
						<view class="fileInfo">
							<view class="fileName">{{fileItem.fileName}}</view>
							<view class="createInfo">{{fileItem.fileDate+' '+fileItem.fileSource}}</view>
						</view>
						<uni-icons type="arrow-down" size="24" style="color: #c9cacc;"></uni-icons>
					</view>
				</uni-swipe-action-item>
			</uni-swipe-action>
		</view>
		<button @click="uploadFile"><uni-icons type="plusempty" size="24" style="color: white"></uni-icons></button>
		<uni-popup ref="alertDialog" type="dialog">
			<uni-popup-dialog type="warn" cancelText="关闭" confirmText="确定" title="通知" content="是否确定下载此文件"
				@confirm="dialogConfirm" @close="dialogClose"></uni-popup-dialog>
		</uni-popup>
	</view>
</template>

<script>
	export default {
		onLoad(options) {
			this.fileTypeId = options.fileTypeId;
		},
		data() {
			return {
				fileType: {
					'1': '身份证',
					'2': '毕业证',
					'3': '学位证',
					'4': '职称/技能证书',
					'5': '劳动合同',
					'6': '保密协议',
					'7': '竞业限制',
					'8': '员工基本信息登记表',
					'9': '法律文书送达信息确认书',
					'10': '重要事项告知书',
					'11': '员工入职手续确认单',
					'12': '离职声明/证明',
					'13': '身体检报告',
					'14': '简历',
				},
				options: [{
					text: '删除',
					style: {
						backgroundColor: '#dd524d'
					}
				}],
				downloadUrl: '',
				fileTypeId: '',
				fileList: [{
						'id': 1,
						'fileName': '简历.docx',
						'fileDate': '2023-08-21',
						'fileSource': '来自入职材料',
						'url': '',
						'pic': '/static/word.svg'
					},
					{
						'id': 2,
						'fileName': '简历2.pdf',
						'fileDate': '2023-08-01',
						'fileSource': '来自手动上传',
						'url': '',
						'pic': '/static/pdf.svg'
					},
					{
						'id': 2,
						'fileName': '简历2.docx',
						'fileDate': '2023-08-01',
						'fileSource': '来自手动上传',
						'url': '',
						'pic': '/static/word.svg'
					},
					{
						'id': 2,
						'fileName': '简历2.docx',
						'fileDate': '2023-08-01',
						'fileSource': '来自手动上传',
						'url': '',
						'pic': '/static/word.svg'
					},
					{
						'id': 2,
						'fileName': '简历2.docx',
						'fileDate': '2023-08-01',
						'fileSource': '来自手动上传',
						'url': '',
						'pic': '/static/word.svg'
					},
					{
						'id': 2,
						'fileName': '简历2.docx',
						'fileDate': '2023-08-01',
						'fileSource': '来自手动上传',
						'url': '',
						'pic': '/static/word.svg'
					},
					{
						'id': 2,
						'fileName': '简历2.docx',
						'fileDate': '2023-08-01',
						'fileSource': '来自手动上传',
						'url': '',
						'pic': '/static/word.svg'
					},
					{
						'id': 2,
						'fileName': '简历2.docx',
						'fileDate': '2023-08-01',
						'fileSource': '来自手动上传',
						'url': '',
						'pic': '/static/word.svg'
					},
					{
						'id': 2,
						'fileName': '简历2.docx',
						'fileDate': '2023-08-01',
						'fileSource': '来自手动上传',
						'url': '',
						'pic': '/static/word.svg'
					},
					{
						'id': 2,
						'fileName': '简历2.docx',
						'fileDate': '2023-08-01',
						'fileSource': '来自手动上传',
						'url': '',
						'pic': '/static/word.svg'
					},
					{
						'id': 2,
						'fileName': '简历2.docx',
						'fileDate': '2023-08-01',
						'fileSource': '来自手动上传',
						'url': '',
						'pic': '/static/word.svg'
					},
					{
						'id': 2,
						'fileName': '简历2.docx',
						'fileDate': '2023-08-01',
						'fileSource': '来自手动上传',
						'url': '',
						'pic': '/static/word.svg'
					},
					{
						'id': 2,
						'fileName': '简历2.docx',
						'fileDate': '2023-08-01',
						'fileSource': '来自手动上传',
						'url': '',
						'pic': '/static/word.svg'
					},
					{
						'id': 2,
						'fileName': '简历2.docx',
						'fileDate': '2023-08-01',
						'fileSource': '来自手动上传',
						'url': '',
						'pic': '/static/word.svg'
					}
				]
			};
		},
		methods: {
			uploadFile() {
				uni.navigateTo({
					url: '/subpkg/uploadFile/uploadFile?fileTypeName=' + String(this.fileType[this.fileTypeId])
				})
			},
			downloadFile(val) {

			},
			dialogToggle(val) {
				this.$refs.alertDialog.open()
				this.downloadUrl = val
			},
			dialogConfirm() {
				console.log('点击确认')
				this.messageText = `点击确认了 ${this.msgType} 窗口`
				this.$refs.alertDialog.close()
			},
			dialogClose() {
				console.log('点击关闭')
			},
			onClick(e) {
				console.log('点击了' + (e.position === 'left' ? '左侧' : '右侧') + e.content.text + '按钮')
			},
			swipeChange(e, index) {
				console.log('当前状态：' + e + '，下标：' + index)
			}
		}
	}
</script>

<style lang="scss">
	.list-container {
		width: 100%;
		height: 100px;
		display: flex;
		flex-direction: row;
		justify-content: space-around;
		align-items: center;
		border-bottom: solid 0.5px #c9cacc;

		.fileName {
			margin-bottom: 5px;
		}

		.createInfo {
			color: gray;
			font-size: 14px;
		}
	}

	button {
		width: 50px;
		height: 50px;
		background-color: blue;
		border-radius: 50px;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		position: fixed;
		bottom: 20px;
		right: 20px;
	}
</style>