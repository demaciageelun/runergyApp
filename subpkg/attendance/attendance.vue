<template>
	<view>
		<view>
			<uni-calendar class="uni-calendar--hook" :selected="info.selected" :showMonth="true" @change="change"
				@monthSwitch="monthSwitch" />
			<view class="total-container">
				<view class="total-title-container"><text>月度考勤汇总</text></view>
				<view class="total-box-container">
					<view class="box-container">
						<view class="color-box" style="background-color: #DAF0FE;"></view>
						<view class="font-box"><text>0</text><text>迟到</text></view>
					</view>
					<view class="box-container">
						<view class="color-box" style="background-color: #FEF2DC;"></view>
						<view class="font-box"><text>0</text><text>早退</text></view>
					</view>
					<view class="box-container">
						<view class="color-box" style="background-color: #FCD9DF;"></view>
						<view class="font-box"><text>0</text><text>旷工</text></view>
					</view>
					<view class="box-container">
						<view class="color-box" style="background-color: #F1E9FE;"></view>
						<view class="font-box"><text>0</text><text>未打卡</text></view>
					</view>
					<view class="box-container">
						<view class="color-box" style="background-color: #E6F6DB;"></view>
						<view class="font-box"><text>0</text><text>出差</text></view>
					</view>
				</view>
<!-- 				<view class="total-title-container"><text>当日考勤</text></view>
				<view class="check-box-container">
					<view class="check-container">
						<text>实际上班时间</text>
						<text>2023-09-01 00:00:00</text>
					</view>
					<view class="check-container">
						<text>实际下班时间</text>
						<text>2023-09-01 00:00:00</text>
					</view>
				</view> -->
			</view>
		</view>
	</view>
</template>

<script>
	/**
	 * 获取任意时间
	 */
	function getDate(date, AddDayCount = 0) {
		if (!date) {
			date = new Date()
		}
		if (typeof date !== 'object') {
			date = date.replace(/-/g, '/')
		}
		const dd = new Date(date)

		dd.setDate(dd.getDate() + AddDayCount) // 获取AddDayCount天后的日期

		const y = dd.getFullYear()
		const m = dd.getMonth() + 1 < 10 ? '0' + (dd.getMonth() + 1) : dd.getMonth() + 1 // 获取当前月份的日期，不足10补0
		const d = dd.getDate() < 10 ? '0' + dd.getDate() : dd.getDate() // 获取当前几号，不足10补0
		return {
			fullDate: y + '-' + m + '-' + d,
			year: y,
			month: m,
			date: d,
			day: dd.getDay()
		}
	}
	export default {
		data() {
			return {
				code: '1010000410',
				showCalendar: false,
				info: {
					lunar: true,
					range: true,
					insert: false,
					selected: [{
						date: '2023-09-01',
						info: '打卡'
					}]
				}
			};
		},
		onReady() {
			this.$nextTick(() => {
				this.showCalendar = true
			})
			// TODO 模拟请求异步同步数据
			setTimeout(() => {
				this.info.date = getDate(new Date(), -30).fullDate
				this.info.startDate = getDate(new Date(), -60).fullDate
				this.info.endDate = getDate(new Date(), 30).fullDate
			}, 2000)
			const currentDate = new Date();
			const year = currentDate.getFullYear(); // 获取当前年份
			const month = currentDate.getMonth() + 1; // 获取当前月份（加1以得到实际月份）
			this.getMonthAttendance(String(year) + '-' + String(month).padStart(2, '0'))
		},
		methods: {
			open() {
				this.$refs.calendar.open()
			},
			close() {
				console.log('弹窗关闭');
			},
			change(e) {
				console.log('change 返回:', e)
				this.getMonthAttendance(String(e['year']) + '-' + String(e['month']).padStart(2, '0'))
			},
			confirm(e) {
				console.log('confirm 返回:', e)
			},
			monthSwitch(e) {
				console.log('monthSwitchs 返回:', e)
				this.getMonthAttendance(String(e['year']) + '-' + String(e['month']).padStart(2, '0'))
			},
			// 获取每个月的出勤情况
			async getMonthAttendance(month) {
				const {
					data: res
				} = await uni.$http.post("/wx/attendance/data", {
					"code": this.code,
					"month": month
				});
				if (res.code != 200) {
					uni.$showMsg(res.msg, 1500, "error")
				} else {
					this.info.selected = res.data.daliy_list
				}
			},
		}
	}
</script>

<style lang="scss">
	page {
		background-color: #f5f5f5;
	}
	.total-container {
		width: 100%;
		background-color: #F7F8FA;
		display: flex;
		flex-direction: column;
		margin-top: 20px;
		padding-bottom: 20px;

		.total-title-container {
			padding-top: 20px;
			margin-bottom: 20px;
			padding-left: 10px;

			text {
				font-size: 24px;
				font-weight: 800;
			}
		}

		.total-box-container {
			width: 100%;
			display: flex;
			flex-direction: row;
			justify-content: space-evenly;
			align-items: center;

			.box-container {
				width: 17%;
				height: 70px;
				background-color: #fff;
				border-radius: 10px;

				.color-box {
					height: 18%;
					border-radius: 10px 10px 0px 0px;
				}

				.font-box {
					display: flex;
					flex-direction: column;
					justify-content: center;
					align-items: center;
					font-size: 14px;
					color: #6A6A6A;

					text:first-child {
						font-size: 20px;
						font-weight: 700;
						color: black;
					}
				}
			}
		}

		.check-box-container {
			width: 100%;
			display: flex;
			flex-direction: row;
			justify-content: space-around;
			align-items: center;

			.check-container {
				border-radius: 10px;
				background-color: #fff;
				width: 45%;
				height: 80px;
				display: flex;
				flex-direction: column;
				justify-content: space-around;
				align-items: center;
				font-size: 14px;
				color: #6A6A6A;

				text:first-child {
					font-size: 20px;
					font-weight: 700;
					color: black;
				}

			}
		}
	}
</style>