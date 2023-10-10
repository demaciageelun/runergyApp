<template>
	<view>
		<view class="step-container">
			<uni-steps :options="list1" active-icon="checkbox" :active="active" />
		</view>
		<view class="container">
			<image src="/static/success.svg"></image>
			<view><text>已完成入职流程，请等待审批!</text></view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				buttonLoading: false,
				active: 3,
				list1: [{
					title: '离职证明'
				},{
					title: '体检报告'
				},{
					title: '简历'
				},{
					title: '完成'
				},],
			};
		}
	}
</script>

<style lang="scss">
	.step-container {
		margin: 50px 0px 50px 0px;
	}
	
.container{
	widt: 100%;
	height: 400px;
	display: flex;
	flex-direction: column;
	justify-content: space-evenly;
	align-items: center;
	image{
		width: 30%;
	}
	text{
		font-size: 18px;
		font-weight: 700;
		color: #6A6A6A;
	}
}
</style>