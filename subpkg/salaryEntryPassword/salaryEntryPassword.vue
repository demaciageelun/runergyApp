<template>
	<view>
		<view class="container">
			<!-- <text class="tip">密码长度8~32位,需包含数字、字母、符合至少2种或以上元素</text> -->
			<input class="password" placeholder="请输入密码" />
			<!-- <input class="password2" placeholder="请再次输入密码" /> -->
			<button type="primary" @click="submit">确认</button>
			<text @click="changePassword">忘记密码？</text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {

			};
		},
		methods:{
			changePassword(){
				uni.navigateTo({
					url: '/subpkg/salaryChangePassword/salaryChangePassword'
				})
			},
			submit(){
				uni.navigateTo({
					url: '/subpkg/employeeSalary/employeeSalary'
				})
			}
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
		.password{
			width: 90%;
			height: 60px;
			border-bottom: 1px solid #eaeaea;
			margin-top: 40px;
		}
		button{
			width: 90%;
			margin-top: 20px;
			margin-bottom: 20px;
		}
	}
</style>