<template>
	<view>
		<view class="step-container">
			<uni-steps :options="list1" active-icon="checkbox" :active="active" />
		</view>
		<view class="form-container">
			<uni-forms ref="valiForm" v-model="valiFormData" label-position="top" label-width="200px">
				<uni-forms-item label="银行卡" required name="candidate_identity_file_info">
					<uni-file-picker v-model="valiFormData.candidate_identity_file_info" fileMediatype="image"
						mode="grid"/>
				</uni-forms-item>
			</uni-forms>
			<button type="primary" :loading="buttonLoading" @click="checkPersonInfo">下一步</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				buttonLoading: false,
				active: 2,
				list1: [{
					title: '离职证明'
				},{
					title: '体检报告'
				},{
					title: '简历'
				},{
					title: '一寸照片'
				},],
				valiFormData: {

				}
			};
		},
		methods: {
			checkPersonInfo() {
				this.buttonLoading = true;
				uni.showToast({
					title: '验证成功',
					duration: 2000,
				});
				this.buttonLoading = false;
				uni.navigateTo({
					url: '/subpkg/uploadOneInchPhoto/uploadOneInchPhoto'
				})
			}
		}
	}
</script>

<style lang="scss">
	.step-container {
		margin: 50px 0px 50px 0px;
	}

	.form-container {
		padding: 15px;
		background-color: #fff;

		button {
			margin-top: 50px;
		}
	}
</style>