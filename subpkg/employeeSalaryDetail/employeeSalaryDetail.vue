<template>
	<view>
		<view class="container">
			<view class="title">
				<image :src="heardPicUrl" class="logo"></image>
				<view class="person-info">
					<text class="userName">{{name}}</text>
					<text class="department">{{deptName}} | {{position}}</text>
				</view>
				<text class="tag" style="color: #1B84FC;" v-if="status==1">未查看</text>
				<text class="tag" style="color: #E99D42;" v-if="status==2">已查看</text>
			</view>
			<view class="salary-container">
				<uni-section class="mb-10" title="薪资明细" type="line"></uni-section>
				<view class="salary-list" v-for="(salaryItem, index) in salaryList" :index="index" :key="index">
					<view style="width: 35%; font-size: 15px;font-weight: 600;"><text>{{salaryItem.title + "："}}</text>
					</view>
					<text style="width: 60%; font-size: 14px; color: gray;">{{salaryItem.unit + salaryItem.value}}</text>
				</view>
			</view>
			<button type="primary" @click="salaryConfirm">薪资确认</button>
		</view>
	</view>
</template>

<script>
	export default {
		onLoad(options) {
			this.period = options.PeriodName;
			this.status = options.wxStatus;
		},
		onReady() {
			this.getMonthSalary()
		},
		data() {
			return {
				heardPicUrl: '/static/face.jpg',
				code:'2010009598',
				name: '',
				deptName: '',
				position: '',
				status: '已查看',
				period: '2023年08月',
				languageType: 'chinese',
				salaryList: []
			};
		},
		methods: {
			salaryConfirm() {
				uni.navigateTo({
					url: '/subpkg/salaryConfirm/salaryConfirm'
				})
			},
			async getMonthSalary() {
				const {
					data: res
				} = await uni.$http.post("/wx/salary/data", {
					"code": this.code,
					"period": this.period,
					"language_type": this.languageType
				});
				if (res.code != 200) {
					uni.$showMsg(res.msg, 1500, "error")
				} else {
					this.salaryList = res.data.salaryData
					this.name = res.data.personData.name
					this.deptName = res.data.personData.deptName
					this.position = res.data.personData.position
				}
			},
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
			width: 90%;
			height: 100px;
			background-color: #fff;
			margin: 25px 0px 25px 0px;
			display: flex;
			flex-direction: row;
			justify-content: space-around;
			align-items: center;

			.logo,
			.tag {
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
			}

			.tag {
				line-height: 75px;
				font-size: 24px;
			}
		}

		.salary-container {
			width: 90%;
			border-radius: 5px;
			background-color: #fff;


			.salary-list {
				width: 100%;
				height: 45px;
				border-bottom: solid 1px #f5f5f5;
				display: flex;
				flex-direction: row;
				justify-content: flex-start;
				align-items: center;
				padding-left: 20px;
			}
		}

		button {
			width: 90%;
			margin-top: 20px;
			margin-bottom: 20px;
		}
	}
</style>