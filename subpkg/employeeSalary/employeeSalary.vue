<template>
	<view>
		<view class="container">
			<view class="title">
				<image :src="heardPicUrl" class="logo"></image>
				<view class="person-info">
					<text class="userName">周为</text>
					<text class="department">信息技术部（IT主管）</text>
				</view>
			</view>
			<view class="year-container">
				<uni-icons type="back" size="24" @click="previousYear"></uni-icons>
				<view>{{nowYear+ ' 年'}}</view>
				<uni-icons type="forward" size="24" @click="nextYear"></uni-icons>
			</view>
			<view class="month-container">
				<view class="month-list" v-for="(monthItem, index) in monthDataList" :index="index" :key="index"
					@click="navigateTo(monthItem.wxStatus, monthItem.PeriodName)">
					<text>{{monthItem.PeriodName}}</text>
					<text
						style="font-size: 12px;background-color: #E6F0D7;color: #81B337; border-radius: 5px;padding: 0px 5px 0px 5px;"
						v-if="monthItem.wxStatus ==1">未查看</text>
					<text
						style="font-size: 12px;background-color: #E1EFFF;color: #1B84FC; border-radius: 5px;padding: 0px 5px 0px 5px;"
						v-if="monthItem.wxStatus ==2">已查看</text>
					<text
						style="font-size: 12px;background-color: #FDF5EC;color: #E99D42; border-radius: 5px;padding: 0px 5px 0px 5px;"
						v-if="monthItem.wxStatus ==4">未生成</text>
					<text
						style="font-size: 12px;background-color: #E5E7F8;color: #0014B7; border-radius: 5px;padding: 0px 5px 0px 5px;"
						v-if="monthItem.wxStatus ==3">未入职</text>
					<uni-icons type="forward" size="18"></uni-icons>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		onReady() {
			this.getNowYear()
			this.getMonthSalaryList()
		},
		data() {
			return {
				heardPicUrl: '/static/face.jpg',
				code: '2010009598',
				nowYear: 2023,
				languageType: 'Chinese',
				monthDataList: []
			};
		},
		methods: {
			getNowYear() {
				let timestamp = Date.parse(new Date());
				let date = new Date(timestamp);
				this.nowYear = date.getFullYear();
			},
			previousYear() {
				//点击获取前一年
				this.nowYear -= 1
				this.getMonthSalaryList()
			},
			nextYear() {
				//点击获取后一年
				this.nowYear += 1
				this.getMonthSalaryList()
			},
			async getMonthSalaryList() {
				const {
					data: res
				} = await uni.$http.post("/wx/salaryList/data", {
					"code": this.code,
					"year": this.nowYear,
					"language_type": this.languageType
				});
				if (res.code != 200) {
					uni.$showMsg(res.msg, 1500, "error")
				} else {
					console.log(res.data);
					if (res.code == 200) {
						this.monthDataList = res.data
					} else {
						uni.$showMsg(res.msg)
					}
				}
			},
			navigateTo(val1, val2) {
				if (val1 == 1 || val1 == 2) {
					uni.navigateTo({
						url: '/subpkg/employeeSalaryDetail/employeeSalaryDetail?PeriodName=' + String(val2).slice(0, 8) +'&wxStatus=' + String(val1)
					})
				} else {
					uni.$showMsg('当前周期暂无薪资数据')
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

		.year-container,
		.month-container {
			width: 90%;
			background-color: #fff;
			border-radius: 5px;
		}

		.year-container {
			height: 50px;
			display: flex;
			flex-direction: row;
			justify-content: center;
			align-items: center;

			.uni-icons {
				margin-left: 10px;
				margin-right: 10px;
			}
		}

		.month-list {
			width: 100%;
			height: 50px;
			display: flex;
			flex-direction: row;
			justify-content: space-evenly;
			align-items: center;
			border: 1px solid #f5f5f5;
		}
	}
</style>