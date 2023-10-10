<template>
	<view>
		<view class="container">
			<text class="tip">密码长度8~32位,需包含数字、字母、符合至少2种或以上元素</text>
			<input class="password" placeholder="请输入密码" />
			<input class="password2" placeholder="请再次输入密码" />
			<button type="primary">确认</button>
			<!-- <text>忘记密码？</text> -->
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {

			};
		}
	}
</script>

<style lang="scss">
	.container{
		width: 100%;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		.tip{
			width: 90%;
			color: #999999;
			margin: 40px 0px 20px 0px;
			font-size: 14px;
		}
		.password,.password2{
			width: 90%;
			height: 60px;
			border-bottom: 1px solid #eaeaea;
		}
		button{
			width: 90%;
			margin-top: 20px;
			margin-bottom: 20px;
		}
	}
</style>