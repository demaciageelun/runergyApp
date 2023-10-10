<template>
	<view>
		<view class="step-container">
			<uni-steps :options="list1" active-icon="checkbox" :active="active" />
		</view>
		<view class="form-container">
			<uni-forms ref="valiForm" v-model="valiFormData" label-position="top" label-width="200px">
				<uni-forms-item label="姓名" required name="candidate_name">
					<uni-easyinput v-model="valiFormData.candidate_name" placeholder="请输入姓名" />
				</uni-forms-item>
				<uni-forms-item label="身份证号码" required name="candidate_identity_no">
					<uni-easyinput v-model="valiFormData.candidate_identity_no" placeholder="请输入身份证" @blur="checkInfo()"
						type="idcard" />
				</uni-forms-item>
				<uni-forms-item label="国籍" required name="candidate_nationality">
					<zxz-uni-data-select v-model="valiFormData.candidate_nationality" :localdata="contryOptions"
						filterable :disabled="isDisabled"></zxz-uni-data-select>
				</uni-forms-item>
				<uni-forms-item label="性别" required name="candidate_sex">
					<uni-data-select v-model="valiFormData.candidate_sex" :localdata="sexOption"
						:disabled="isDisabled"></uni-data-select>
				</uni-forms-item>
				<uni-forms-item label="出生日期" required name="candidate_birthday">
					<uni-datetime-picker type="date" :clear-icon="false" v-model="valiFormData.candidate_birthday"
						:disabled="isDisabled" />
				</uni-forms-item>
				<uni-forms-item label="民族" required name="candidate_nation_id">
					<uni-data-select v-model="valiFormData.candidate_nation_id" :localdata="nationOptions"
						:disabled="isDisabled"></uni-data-select>
				</uni-forms-item>
				<uni-forms-item label="婚姻状况" required name="candidate_marriage_status">
					<uni-data-select v-model="valiFormData.candidate_marriage_status" :localdata="marriageOptions"
						:disabled="isDisabled"></uni-data-select>
				</uni-forms-item>
				<uni-forms-item label="邮箱" name="candidate_email">
					<uni-easyinput :disabled="isDisabled" v-model="valiFormData.candidate_email" placeholder="请输入邮箱" />
				</uni-forms-item>

				<uni-forms-item label="籍贯" required name="candidate_nation_place_id">
					<uni-data-picker placeholder="请选择籍贯" popup-title="请选择所在地区" :localdata="nationPlaceOption"
						:readonly="isDisabled" v-model="valiFormData.candidate_nation_place_id"></uni-data-picker>
				</uni-forms-item>
				<uni-forms-item label="法定送达地址(户籍地址)" required name="candidate_nation_address">
					<uni-easyinput v-model="valiFormData.candidate_nation_address" placeholder="请按省、地级市、区、镇、小区，精确到门牌号填写"
						placeholderStyle="font-size:10px" :disabled="isDisabled" />
				</uni-forms-item>
				<uni-forms-item label="现居住地址" required name="candidate_now_address">
					<uni-easyinput v-model="valiFormData.candidate_now_address" placeholder="请输入现居住地址"
						:disabled="isDisabled" />
				</uni-forms-item>
				<uni-forms-item label="联系电话" required name="candidate_phone">
					<uni-easyinput v-model="valiFormData.candidate_phone" placeholder="请输入联系电话"
						:disabled="isDisabled" />
				</uni-forms-item>
				<uni-forms-item label="政治面貌" required name="candidate_political_status">
					<uni-data-select v-model="valiFormData.candidate_political_status" :localdata="politicalOptions"
						:disabled="isDisabled"></uni-data-select>
				</uni-forms-item>
				<uni-forms-item label="紧急联系人" required name="candidate_emergency_contact">
					<uni-easyinput v-model="valiFormData.candidate_emergency_contact" placeholder="请输入紧急联系人"
						:disabled="isDisabled" />
				</uni-forms-item>
				<uni-forms-item label="与本人关系" required name="candidate_emergency_contact_relation">
					<uni-data-select v-model="valiFormData.candidate_emergency_contact_relation"
						:localdata="relationOptions" :disabled="isDisabled"></uni-data-select>
				</uni-forms-item>
				<uni-forms-item label="紧急联系人工作单位" required name="candidate_emergency_contact_company">
					<uni-easyinput v-model="valiFormData.candidate_emergency_contact_company" placeholder="请输入紧急联系人工作单位"
						:disabled="isDisabled" />
				</uni-forms-item>
				<uni-forms-item label="紧急联系人联系方式" required name="candidate_emergency_contact_phone">
					<uni-easyinput v-model="valiFormData.candidate_emergency_contact_phone" placeholder="请输入紧急联系人联系方式"
						:disabled="isDisabled" />
				</uni-forms-item>
				<uni-forms-item label="紧急联系人2" required name="candidate_emergency_contact_2">
					<uni-easyinput v-model="valiFormData.candidate_emergency_contact_2" placeholder="请输入紧急联系人2"
						:disabled="isDisabled" />
				</uni-forms-item>
				<uni-forms-item label="与本人关系" required name="candidate_emergency_contact_relation_2">
					<uni-data-select v-model="valiFormData.candidate_emergency_contact_relation_2"
						:localdata="relationOptions" :disabled="isDisabled"></uni-data-select>
				</uni-forms-item>
				<uni-forms-item label="紧急联系人2工作单位" required name="candidate_emergency_contact_company_2">
					<uni-easyinput v-model="valiFormData.candidate_emergency_contact_company_2"
						placeholder="请输入紧急联系人2工作单位" :disabled="isDisabled" />
				</uni-forms-item>
				<uni-forms-item label="紧急联系人2联系方式" required name="candidate_emergency_contact_phone_2">
					<uni-easyinput v-model="valiFormData.candidate_emergency_contact_phone_2"
						placeholder="请输入紧急联系人2联系方式" :disabled="isDisabled" />
				</uni-forms-item>
				<uni-forms-item label="第一学历" required name="candidate_first_degree_id">
					<uni-data-select v-model="valiFormData.candidate_first_degree_id" :localdata="firstDegreeOptions"
						:disabled="isDisabled"></uni-data-select>
				</uni-forms-item>
				<uni-forms-item label="第一学历学校名称" required name="candidate_first_degree_school">
					<uni-easyinput v-model="valiFormData.candidate_first_degree_school" placeholder="第一学历学校名称"
						:disabled="isDisabled" />
				</uni-forms-item>
				<uni-forms-item label="第一学历专业" required name="candidate_first_degree_major">
					<uni-easyinput v-model="valiFormData.candidate_first_degree_major" placeholder="第一学历专业"
						:disabled="isDisabled" />
				</uni-forms-item>
				<uni-forms-item label="第一学历教育方式" required name="candidate_first_degree_type">
					<uni-data-select v-model="valiFormData.candidate_first_degree_type"
						:localdata="firstDegreeTypeOptions" :disabled="true" :clear="false"></uni-data-select>
				</uni-forms-item>
				<uni-forms-item label="第一学历毕业日期" required name="candidate_first_degree_graduate_date">
					<uni-datetime-picker type="date" :clear-icon="false"
						v-model="valiFormData.candidate_first_degree_graduate_date" :disabled="isDisabled" readonly />
				</uni-forms-item>
				<uni-forms-item label="进修学历" name="candidate_train_degree">
					<uni-easyinput v-model="valiFormData.candidate_train_degree" placeholder="进修学历"
						:disabled="isDisabled" />
				</uni-forms-item>
				<uni-forms-item label="进修学历学校名称" name="candidate_train_degree_school">
					<uni-easyinput v-model="valiFormData.candidate_train_degree_school" placeholder="进修学历学校名称"
						:disabled="isDisabled" />
				</uni-forms-item>
				<uni-forms-item label="进修学历专业" name="candidate_train_degree_major">
					<uni-easyinput v-model="valiFormData.candidate_train_degree_major" placeholder="进修学历专业"
						:disabled="isDisabled" />
				</uni-forms-item>
				<uni-forms-item label="进修学历教育方式" name="candidate_train_degree_type">
					<uni-data-select v-model="valiFormData.candidate_train_degree_type" :localdata="trainDegreeOptions"
						:disabled="isDisabled"></uni-data-select>
				</uni-forms-item>
				<uni-forms-item label="进修学历毕业日期" name="candidate_train_degree_graduate_date">
					<uni-datetime-picker type="date" :clear-icon="false"
						v-model="valiFormData.candidate_train_degree_graduate_date" :disabled="isDisabled" />
				</uni-forms-item>
				<uni-forms-item label="工作经历">
					<view v-for="(item, index) in valiFormData.candidate_work_experience_info" :key="item.id">
						<uni-datetime-picker type="date" :clear-icon="false" v-model="item.work_experience_hire_date"
							placeholder="选择工作开始日期" style="margin-bottom: 10px" :disabled="isDisabled" />
						<uni-datetime-picker type="date" :clear-icon="false"
							v-model="item.work_experience_departure_date" placeholder="选择工作结束日期"
							style="margin-bottom: 10px" :disabled="isDisabled" />
						<uni-easyinput :disabled="isDisabled" v-model="item.work_experience_company"
							style="margin-bottom: 10px" placeholder="请输入公司名称" />
						<uni-easyinput :disabled="isDisabled" v-model="item.work_experience_position"
							style="margin-bottom: 10px" placeholder="请输入职位" />

						<button :disabled="isDisabled" type="primary" @click="handleDelWork(index)" style="
			          width: 80%;
			          height: 30px;
			          font-size: 15px;
			          line-height: 30px;
			          margin-bottom: 10px;
			        ">
							点击删除工作经历
						</button>
						<view style="
			          width: 100%;
			          border-bottom: 1px solid #ccc;
			          margin-bottom: 10px;
			        "></view>
					</view>
					<button :disabled="isDisabled" type="primary" @click="handleAddWork" style="
			        width: 80%;
			        height: 30px;
			        font-size: 15px;
			        line-height: 30px;
			      ">
						点击添加工作经历
					</button>
				</uni-forms-item>
				<!-- <uni-forms-item label="工作地" required name="candidate_work_place">
			    <uni-easyinput
			      v-model="valiFormData.candidate_work_place"
			      :disabled="isDisabled"
			      placeholder="请输入工作地" />
			  </uni-forms-item> -->
				<uni-forms-item label="银行卡号" name="candidate_bank_no">
					<uni-easyinput v-model="valiFormData.candidate_bank_no" placeholder="请输入银行卡号"
						:disabled="isDisabled" />
				</uni-forms-item>
				<uni-forms-item label="开户银行" name="candidate_bank_deposit">
					<uni-easyinput v-model="valiFormData.candidate_bank_deposit" placeholder="请输入开户银行(例:中国农业银行)"
						:disabled="isDisabled" />
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
				active: 1,
				list1: [{
					title: '身份确认'
				}, {
					title: '信息填写'
				}, {
					title: '身份证上传'
				}, {
					title: '毕业证上传'
				}],
				valiFormData: {
					candidate_work_experience_info: [{
						work_experience_hire_date: "",
						work_experience_departure_date: "",
						work_experience_company: "",
						work_experience_position: "",
					}, ],
					id: "",
					candidate_name: "",
					candidate_identity_no: "",

					// candidate_work_place: "",
					candidate_sex: "",
					candidate_phone: "",
					candidate_first_degree_id: "",
					candidate_first_degree_school: "",
					candidate_first_degree_major: "",
					candidate_first_degree_type: "全日制",
					candidate_first_degree_graduate_date: "",
					candidate_train_degree: "",
					candidate_train_degree_school: "",
					candidate_train_degree_major: "",
					candidate_train_degree_type: "",
					candidate_train_degree_graduate_date: "",
					candidate_birthday: "",
					candidate_nationality: "",
					candidate_nation_id: "",
					candidate_marriage_status: "",
					candidate_nation_place_id: "",
					candidate_political_status: "",
					candidate_nation_address: "",
					candidate_now_address: "",
					candidate_emergency_contact: "",
					candidate_emergency_contact_relation: "",
					candidate_emergency_contact_company: "",
					candidate_emergency_contact_phone: "",
					candidate_emergency_contact_2: "",
					candidate_emergency_contact_relation_2: "",
					candidate_emergency_contact_company_2: "",
					candidate_emergency_contact_phone_2: "",
					candidate_bank_no: "",
					candidate_bank_deposit: "",
					candidate_identity_file_info: [],
					candidate_diploma_file_info: [],
					candidate_degree_file_info: [],
					candidate_bank_card_file_info: [],
					candidate_title_or_skill_file_info: [],
					candidate_leave_certificate_file_info: [],
					candidate_medical_report_file_info: [],
					candidate_resume_file_info: [],
					candidate_photo_file_info: [],
				},
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
					url: '/subpkg/uploadIdCard/uploadIdCard'
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