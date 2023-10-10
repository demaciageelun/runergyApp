<script>
	export default {
		// app.vue
		globalData: {
			privacyContractName: '', //隐私协议名称 是接口生成的！
			showPrivacy: false //全局控制弹窗显隐
		},
		onLaunch() {
			const that = this;
			wx.getPrivacySetting({
				success(res) {
					console.log(res)
					console.log('是否需要授权：', res.needAuthorization, '隐私协议的名称为：', res.privacyContractName);
					if (res.needAuthorization) {
						that.globalData.privacyContractName = res.privacyContractName;
						that.globalData.showPrivacy = true;
					} else {
						that.globalData.showPrivacy = false;
					}
				}
			});
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style>
	/*每个页面公共css */
</style>