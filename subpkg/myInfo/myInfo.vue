<template>
  <view>
    <view class="container">
      <view class="title">
        <image :src="heardPicUrl" class="logo"></image>
        <view class="person-info">
          <view class="person-info-top">
            <text class="userName">周为</text>
            <text class="employeeTime">在职3年05个月</text>
          </view>
          <text class="department">信息技术部 | IT主管</text>
        </view>
      </view>
      <view class="personalInfo">
        <uni-forms
          ref="valiForm"
          v-model="valiFormData"
          label-position="top"
          label-width="200px">
          <uni-forms-item
            :label="placeholder.employee_sex"
            required
            name="employee_name">
            <uni-easyinput v-model="valiFormData.employee_sex" disabled />
          </uni-forms-item>
          <uni-forms-item
            :label="placeholder.employee_nation__nation_name"
            required
            name="employee_nation__nation_name">
            <uni-easyinput
              v-model="valiFormData.employee_nation__nation_name"
              disabled />
          </uni-forms-item>
          <uni-forms-item
            :label="placeholder.employee_identity_no"
            required
            name="employee_identity_no">
            <uni-easyinput
              v-model="valiFormData.employee_identity_no"
              disabled />
          </uni-forms-item>
          <uni-forms-item
            :label="placeholder.employee_identity_no_effective_date"
            required
            name="employee_identity_no_effective_date">
            <uni-datetime-picker
              type="date"
              :placeholder="placeholder.employee_please_choose"
              :confirmBottom="placeholder.confirm"
              v-model="valiFormData.employee_identity_no_effective_date" />
          </uni-forms-item>
          <uni-forms-item
            :label="placeholder.employee_identity_no_failre_date"
            required
            name="employee_identity_no_failre_date">
            <uni-datetime-picker
              type="date"
              :confirmBottom="placeholder.confirm"
              :placeholder="placeholder.employee_please_choose"
              v-model="valiFormData.employee_identity_no_failre_date" />
          </uni-forms-item>
          <uni-forms-item
            :label="placeholder.employee_birthday"
            required
            name="employee_birthday">
            <uni-datetime-picker
              type="date"
              :confirmBottom="placeholder.confirm"
              :placeholder="placeholder.employee_please_choose"
              v-model="valiFormData.employee_birthday"
              disabled />
          </uni-forms-item>
          <uni-forms-item
            :label="placeholder.employee_email"
            required
            name="employee_email">
            <uni-easyinput v-model="valiFormData.employee_email" />
          </uni-forms-item>
          <uni-forms-item
            :label="placeholder.employee_marriage_status"
            required
            name="employee_marriage_status">
            <uni-data-select
              :placeholder="placeholder.employee_please_choose"
              v-model="valiFormData.employee_marriage_status"
              :localdata="marriageOptions"></uni-data-select>
          </uni-forms-item>
          <uni-forms-item
            :label="placeholder.employee_nation_address"
            required
            name="employee_nation_address">
            <uni-easyinput
              type="textarea"
              v-model="valiFormData.employee_nation_address" />
          </uni-forms-item>
          <uni-forms-item
            :label="placeholder.employee_now_address"
            required
            name="employee_now_address">
            <uni-easyinput
              type="textarea"
              v-model="valiFormData.employee_now_address" />
          </uni-forms-item>
          <uni-forms-item
            :label="placeholder.employee_phone"
            required
            name="employee_phone">
            <uni-easyinput
              type="number"
              v-model="valiFormData.employee_phone" />
          </uni-forms-item>
          <uni-forms-item
            :label="placeholder.employee_political_status"
            required
            name="employee_political_status">
            <uni-data-select
              :placeholder="placeholder.employee_please_choose"
              v-model="valiFormData.employee_political_status"
              :localdata="politicalOptions"></uni-data-select>
          </uni-forms-item>
          <uni-forms-item
            :label="placeholder.employee_emergency_contact"
            required
            name="employee_emergency_contact">
            <uni-easyinput v-model="valiFormData.employee_emergency_contact" />
          </uni-forms-item>
          <uni-forms-item
            :label="placeholder.employee_emergency_contact_relation"
            required
            name="employee_emergency_contact_relation">
            <uni-data-select
              v-model="valiFormData.employee_emergency_contact_relation"
              :placeholder="placeholder.employee_please_choose"
              :localdata="relationOptions"></uni-data-select>
          </uni-forms-item>
          <uni-forms-item
            :label="placeholder.employee_emergency_contact_phone"
            required
            name="employee_emergency_contact_phone">
            <uni-easyinput
              type="number"
              v-model="valiFormData.employee_emergency_contact_phone" />
          </uni-forms-item>
          <uni-forms-item
            :label="placeholder.employee_first_degree_id"
            required
            name="employee_first_degree_id">
            <uni-data-select
              :placeholder="placeholder.employee_please_choose"
              v-model="valiFormData.employee_first_degree_id"
              :localdata="firstDegreeOptions"></uni-data-select>
          </uni-forms-item>
          <uni-forms-item
            :label="placeholder.employee_first_degree_school"
            required
            name="employee_first_degree_school">
            <uni-easyinput
              v-model="valiFormData.employee_first_degree_school"
              :placeholder="placeholder.employee_first_degree_school" />
          </uni-forms-item>
          <uni-forms-item
            :label="placeholder.employee_first_degree_major"
            required
            name="employee_first_degree_major">
            <uni-easyinput
              v-model="valiFormData.employee_first_degree_major"
              :placeholder="placeholder.employee_first_degree_major" />
          </uni-forms-item>
          <uni-forms-item
            :label="placeholder.employee_first_degree_type"
            required
            name="employee_first_degree_type">
            <uni-data-select
              :placeholder="placeholder.employee_please_choose"
              v-model="valiFormData.employee_first_degree_type"
              :localdata="firstDegreeTypeOptions"
              :disabled="true"
              :clear="false"></uni-data-select>
          </uni-forms-item>
          <uni-forms-item
            :label="placeholder.employee_first_degree_graduate_date"
            required
            name="employee_first_degree_graduate_date">
            <uni-datetime-picker
              type="date"
              :confirmBottom="placeholder.confirm"
              :placeholder="placeholder.employee_please_choose"
              :clear-icon="false"
              v-model="valiFormData.employee_first_degree_graduate_date"
              readonly />
          </uni-forms-item>
          <uni-forms-item
            :label="placeholder.employee_train_degree"
            name="employee_train_degree">
            <uni-easyinput
              v-model="valiFormData.employee_train_degree"
              :placeholder="placeholder.employee_train_degree" />
          </uni-forms-item>
          <uni-forms-item
            :label="placeholder.employee_train_degree_school"
            name="employee_train_degree_school">
            <uni-easyinput
              v-model="valiFormData.employee_train_degree_school"
              :placeholder="placeholder.employee_train_degree_school" />
          </uni-forms-item>
          <uni-forms-item
            :label="placeholder.employee_train_degree_major"
            name="employee_train_degree_major">
            <uni-easyinput
              v-model="valiFormData.employee_train_degree_major"
              :placeholder="placeholder.employee_train_degree_major" />
          </uni-forms-item>
          <uni-forms-item
            :label="placeholder.employee_train_degree_type"
            name="employee_train_degree_type">
            <uni-data-select
              :placeholder="placeholder.employee_please_choose"
              v-model="valiFormData.employee_train_degree_type"
              :localdata="trainDegreeOptions"></uni-data-select>
          </uni-forms-item>
          <uni-forms-item
            :label="placeholder.employee_train_degree_graduate_date"
            name="employee_train_degree_graduate_date">
            <uni-datetime-picker
              type="date"
              :confirmBottom="placeholder.confirm"
              :placeholder="placeholder.employee_please_choose"
              :clear-icon="false"
              v-model="valiFormData.employee_train_degree_graduate_date" />
          </uni-forms-item>
          <uni-forms-item
            :label="placeholder.employee_bank_no"
            required
            name="employee_bank_no">
            <uni-easyinput v-model="valiFormData.employee_bank_no" />
          </uni-forms-item>
          <uni-forms-item
            :label="placeholder.employee_bank_deposit"
            required
            name="employee_bank_deposit">
            <uni-easyinput v-model="valiFormData.employee_bank_deposit" />
          </uni-forms-item>
        </uni-forms>
        <button type="primary" @click="handleSubmit">
          {{ placeholder.employee_submit_button }}
        </button>
      </view>
    </view>
  </view>
</template>
<script>
import { $http } from "@escook/request-miniprogram";
export default {
  data() {
    return {
      language: "Chinese",
      heardPicUrl: "/static/face.jpg",
      placeholder: {
        employee_bank_deposit: "开户行",
        employee_bank_no: "银行卡号",
        employee_birthday: "出生日期",
        employee_email: "个人邮箱",
        employee_emergency_contact: "紧急联系人",
        employee_emergency_contact_phone: "紧急联系人电话",
        employee_emergency_contact_relation: "紧急联系人关系",
        employee_first_degree__edu_degree_name: "第一学历",
        employee_first_degree_graduate_date: "第一学历毕业日期",
        employee_first_degree_major: "第一学历专业",
        employee_first_degree_school: "第一学历学校名称",
        employee_first_degree_type: "第一学历教育方式",
        employee_identity_no: "身份证号",
        employee_identity_no_effective_date: "身份证生效日期",
        employee_identity_no_failre_date: "身份证失效日期",
        employee_marriage_status: "婚姻状况",
        employee_nation__nation_name: "民族",
        employee_nation_address: "户籍地址",
        employee_now_address: "现住址",
        employee_phone: "电话号码",
        employee_political_status: "政治面貌",
        employee_sex: "性别",
        employee_train_degree: "进修学历",
        employee_train_degree_graduate_date: "进修学历毕业日期",
        employee_train_degree_major: "进修学历专业",
        employee_train_degree_school: "进修学历学校名称",
        employee_train_degree_type: "进修学历教育方式",
        employee_submit_button: "提交修改申请",
        employee_please_choose: "请选择",
        confirm: "确认",
      },
      valiFormData: {
        id: "",
        employee_name: "",
        employee_sex: "",
        employee_nation__nation_name: "",
        employee_identity_no: "",
        employee_identity_no_effective_date: "",
        employee_identity_no_failre_date: "",
        employee_birthday: "",
        employee_email: "",
        employee_marriage_status: "1",
        employee_nation_address: "",
        // employee_nation_address_concrete: "",
        employee_now_address: "",
        employee_phone: 0,
        employee_political_status: "",
        employee_nationality: "",
        employee_emergency_contact: "",
        employee_emergency_contact_relation: "",
        employee_emergency_contact_phone: "",
        employee_first_degree_id: "",
        employee_first_degree_school: "",
        employee_first_degree_major: "",
        employee_first_degree_type: "",
        employee_first_degree_graduate_date: "",
        employee_train_degree: "",
        employee_train_degree_school: "",
        employee_train_degree_major: "",
        employee_train_degree_type: "",
        employee_train_degree_graduate_date: "",
        employee_bank_no: "",
        employee_bank_deposit: "",
      },

      // 校验规则
      rules: {
        employee_sex: {
          rules: [
            {
              required: true,
              errorMessage: "性别不能为空",
            },
          ],
        },
        employee_nation__nation_name: {
          rules: [
            {
              required: true,
              errorMessage: "民族不能为空",
            },
          ],
        },
        employee_identity_no: {
          rules: [
            {
              required: true,
              errorMessage: "身份证号不能为空",
            },
          ],
        },
        employee_identity_no_effective_date: {
          rules: [
            {
              required: true,
              errorMessage: "身份证生效日期不能为空",
            },
          ],
        },
        employee_identity_no_failre_date: {
          rules: [
            {
              required: true,
              errorMessage: "身份证失效日期不能为空",
            },
          ],
        },
        employee_birthday: {
          rules: [
            {
              required: true,
              errorMessage: "出生日期不能为空",
            },
          ],
        },
        employee_email: {
          rules: [
            {
              required: true,
              errorMessage: "出生日期不能为空",
            },
          ],
        },
        employee_marriage_status: {
          rules: [
            {
              required: true,
              errorMessage: "婚姻状况不能为空",
            },
          ],
        },
        employee_nation_address: {
          rules: [
            {
              required: true,
              errorMessage: "户籍地址不能为空",
            },
          ],
        },
        employee_now_address: {
          rules: [
            {
              required: true,
              errorMessage: "现住址不能为空",
            },
          ],
        },
        employee_phone: {
          rules: [
            {
              required: true,
              errorMessage: "电话号码不能为空",
            },
          ],
        },
        employee_political_status: {
          rules: [
            {
              required: true,
              errorMessage: "政治面貌不能为空",
            },
          ],
        },
        employee_emergency_contact: {
          rules: [
            {
              required: true,
              errorMessage: "紧急联系人不能为空",
            },
          ],
        },
        employee_emergency_contact_relation: {
          rules: [
            {
              required: true,
              errorMessage: "紧急联系人关系不能为空",
            },
          ],
        },
        employee_emergency_contact_phone: {
          rules: [
            {
              required: true,
              errorMessage: "紧急联系人电话不能为空",
            },
          ],
        },
        employee_first_degree_id: {
          rules: [
            {
              required: true,
              errorMessage: "第一学历不能为空",
            },
          ],
        },
        employee_first_degree_school: {
          rules: [
            {
              required: true,
              errorMessage: "第一学历学校名称不能为空",
            },
          ],
        },
        employee_first_degree_major: {
          rules: [
            {
              required: true,
              errorMessage: "第一学历专业不能为空",
            },
          ],
        },
        employee_first_degree_type: {
          rules: [
            {
              required: true,
              errorMessage: "第一学历教育方式不能为空",
            },
          ],
        },
        employee_first_degree_graduate_date: {
          rules: [
            {
              required: true,
              errorMessage: "第一学历毕业日期不能为空",
            },
          ],
        },
        employee_bank_no: {
          rules: [
            {
              required: true,
              errorMessage: "银行卡号不能为空",
            },
          ],
        },
        employee_bank_deposit: {
          rules: [
            {
              required: true,
              errorMessage: "开户行不能为空",
            },
          ],
        },
      },

      nationOptions: [],
      marriageOptions: [],
      politicalOptions: [],
      firstDegreeOptions: [],
      firstDegreeTypeOptions: [],
      trainDegreeOptions: [],
      relationOptions: [
        {
          text: "父亲",
          value: "父亲",
        },
        {
          text: "母亲",
          value: "母亲",
        },
        {
          text: "夫妻",
          value: "夫妻",
        },
        {
          text: "儿子",
          value: "儿子",
        },
        {
          text: "女儿",
          value: "女儿",
        },
        {
          text: "兄妹",
          value: "兄妹",
        },
        {
          text: "其他",
          value: "其他",
        },
      ],
    };
  },
  onReady() {
    // 设置自定义表单校验规则，必须在节点渲染完毕后执行
    this.$refs.valiForm.setRules(this.rules);
  },
  onShow() {
    this.language = localStorage.getItem("language");
    $http
      .post("/wx/get_info", { language: this.language, code: "123123" })
      .then((res) => {
        console.log(res);
        for (let key in this.valiFormData) {
          this.valiFormData[key] = res.data.data[key];
        }
        this.placeholder = res.data.column;
      });
  },
  onLoad() {
    $http.post("/wx/drop_down_menu").then((res) => {
      let data = res.data.data;
      this.politicalOptions = data.politicalOptions;
      this.marriageOptions = data.marriageOptions;
      this.trainDegreeOptions = data.trainDegreeOptions;
      this.firstDegreeTypeOptions = data.firstDegreeTypeOptions;
      this.firstDegreeOptions = data.firstDegreeOptions;
      this.sexOption = data.sexOption;
    });
  },
  methods: {
    handleSubmit() {
      $http.post("/wx/edit_info", this.valiFormData).then((res) => {
        console.log(res);
        uni.$showMsg("提交成功");
      });
    },
  },
};
</script>
<style lang="scss" scoped>
page {
  background-color: #f5f5f5;
}

::v-deep .uni-forms {
  width: 100%;
}

::v-deep .uni-forms-item.is-direction-top .uni-forms-item__label {
  white-space: nowrap;
}

.container {
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  .title {
    border-radius: 5px;
    width: 94%;
    height: 100px;
    background-color: #fff;
    margin: 10px 0px 10px 0px;
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
    align-items: center;

    .logo {
      width: 75px;
      height: 75px;
      border-radius: 50px;
      margin-left: 15px;
    }

    .person-info {
      margin-left: 15px;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: flex-start;

      .person-info-top {
        margin-bottom: 10px;
        display: flex;
        flex-direction: row;
        justify-content: center;
        align-items: center;

        .userName {
          font-weight: 700;
        }

        .employeeTime {
          margin-left: 15px;
          padding: 1px 5px 0px 5px;
          background-color: #d7eaff;
          color: #3894ff;
          border: solid 1px #3894ff;
          border-radius: 5px;
        }
      }

      .department {
        color: #c2c1c1;
        font-size: 14px;
      }
    }
  }

  .personalInfo {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background-color: #fff;
    width: 94%;

    .uni-forms {
      width: 90%;
    }
    button {
      width: 90%;
      margin-top: 20px;
      margin-bottom: 40px;
    }
  }
}
</style>
