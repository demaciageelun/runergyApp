<template>
	<view>
		<privacyPopup></privacyPopup>

		<view class="step-container">
			<uni-steps :options="list1" active-icon="checkbox" :active="active" />
		</view>
		<view class="form-container">
			<uni-forms ref="valiForm" v-model="valiFormData" label-position="top" label-width="200px">
				<uni-forms-item label="姓名" required name="candidate_name">
					<uni-easyinput v-model="valiFormData.candidate_name" :placeholder="placeholder" />
				</uni-forms-item>
				<uni-forms-item label="身份证" required name="candidate_name">
					<uni-easyinput v-model="valiFormData.candidate_name" placeholder="请输入身份证" />
				</uni-forms-item>
				<uni-forms-item label="国籍" required name="candidate_nationality">
					<zxz-uni-data-select v-model="valiFormData.candidate_nationality" :localdata="contryOptions"
						filterable></zxz-uni-data-select>
				</uni-forms-item>
			</uni-forms>
			<button type="primary" :loading="buttonLoading" @click="checkPersonInfo">下一步</button>
		</view>
	</view>
</template>

<script>
	import privacyPopup from '../../components/privacyPopup.vue';
	export default {
		components: {
			privacyPopup
		},

		data() {
			return {
				placeholder: '123',
				buttonLoading: false,
				active: 0,
				list1: [{
					title: '身份确认'
				}, {
					title: '信息填写'
				}, {
					title: '身份证上传'
				}, {
					title: '毕业证上传'
				}],
				contryOptions: [{
						text: "中国",
						value: "中国"
					}, {
						text: "Afghanistan",
						value: "阿富汗"
					},
					{
						text: "Albania",
						value: "阿尔巴尼亚"
					},
					{
						text: "Algeria",
						value: "阿尔及利亚"
					},
					{
						text: "Andorra",
						value: "安道尔"
					},
					{
						text: "Angola",
						value: "安哥拉"
					},
					{
						text: "AntiguaandBarbuda",
						value: "安提瓜和巴布达"
					},
					{
						text: "Argentina",
						value: "阿根廷"
					},
					{
						text: "Armenia",
						value: "亚美尼亚"
					},
					{
						text: "Australia",
						value: "澳大利亚"
					},
					{
						text: "Austria",
						value: "奥地利"
					},
					{
						text: "Azerbaijan",
						value: "阿塞拜疆"
					},
					{
						text: "TheBahamas",
						value: "巴哈马"
					},
					{
						text: "Bahrain",
						value: "巴林"
					},
					{
						text: "Bangladesh",
						value: "孟加拉国"
					},
					{
						text: "Barbados",
						value: "巴巴多斯"
					},
					{
						text: "Belarus",
						value: "白俄罗斯"
					},
					{
						text: "Belgium",
						value: "比利时"
					},
					{
						text: "Belize",
						value: "伯利兹"
					},
					{
						text: "Benin",
						value: "贝宁"
					},
					{
						text: "Bhutan",
						value: "不丹"
					},
					{
						text: "Bolivia",
						value: "玻利维亚"
					},
					{
						text: "BosniaandHerzegovina",
						value: "波斯尼亚和黑塞哥维那"
					},
					{
						text: "Botswana",
						value: "博茨瓦纳"
					},
					{
						text: "Brazil",
						value: "巴西"
					},
					{
						text: "Brunei",
						value: "文莱"
					},
					{
						text: "Bulgaria",
						value: "保加利亚"
					},
					{
						text: "BurkinaFaso",
						value: "布基纳法索"
					},
					{
						text: "Burundi",
						value: "布隆迪"
					},
					{
						text: "Cameroon",
						value: "喀麦隆"
					},
					{
						text: "Canada",
						value: "加拿大"
					},
					{
						text: "CapeVerde",
						value: "佛得角"
					},
					{
						text: "CentralAfricanRepublic",
						value: "中非共和国"
					},
					{
						text: "Chad",
						value: "乍得"
					},
					{
						text: "Chile",
						value: "智利"
					},
					{
						text: "Colombia",
						value: "哥伦比亚"
					},
					{
						text: "Comoros",
						value: "科摩罗"
					},
					{
						text: "Congo,Brazzaville",
						value: "刚果（布拉柴维尔）"
					},
					{
						text: "Congo,Kinshasa",
						value: "刚果（金）"
					},
					{
						text: "CostaRica",
						value: "哥斯达黎加"
					},
					{
						text: "Croatia",
						value: "克罗地亚"
					},
					{
						text: "Cuba",
						value: "古巴"
					},
					{
						text: "Cyprus",
						value: "塞浦路斯"
					},
					{
						text: "CzechRepublic",
						value: "捷克共和国"
					},
					{
						text: "Denmark",
						value: "丹麦"
					},
					{
						text: "Djibouti",
						value: "吉布提"
					},
					{
						text: "Dominica",
						value: "多米尼克"
					},
					{
						text: "DominicanRepublic",
						value: "多米尼加共和国"
					},
					{
						text: "EastTimor",
						value: "东帝汶"
					},
					{
						text: "Ecuador",
						value: "厄瓜多尔"
					},
					{
						text: "Egypt",
						value: "埃及"
					},
					{
						text: "ElSalvador",
						value: "萨尔瓦多"
					},
					{
						text: "EquatorialGuinea",
						value: "赤道几内亚"
					},
					{
						text: "Eritrea",
						value: "厄立特里亚"
					},
					{
						text: "Estonia",
						value: "爱沙尼亚"
					},
					{
						text: "Ethiopia",
						value: "埃塞俄比亚"
					},
					{
						text: "Fiji",
						value: "斐济"
					},
					{
						text: "Finland",
						value: "芬兰"
					},
					{
						text: "France",
						value: "法国"
					},
					{
						text: "Gabon",
						value: "加蓬"
					},
					{
						text: "TheGambia",
						value: "冈比亚"
					},
					{
						text: "Georgia",
						value: "格鲁吉亚"
					},
					{
						text: "Germany",
						value: "德国"
					},
					{
						text: "Ghana",
						value: "加纳"
					},
					{
						text: "Greece",
						value: "希腊"
					},
					{
						text: "Grenada",
						value: "格林纳达"
					},
					{
						text: "Guatemala",
						value: "危地马拉"
					},
					{
						text: "Guinea",
						value: "几内亚"
					},
					{
						text: "Guinea-Bissau",
						value: "几内亚比绍"
					},
					{
						text: "Guyana",
						value: "圭亚那"
					},
					{
						text: "Haiti",
						value: "海地"
					},
					{
						text: "Honduras",
						value: "洪都拉斯"
					},
					{
						text: "Hungary",
						value: "匈牙利"
					},
					{
						text: "Iceland",
						value: "冰岛"
					},
					{
						text: "India",
						value: "印度"
					},
					{
						text: "Indonesia",
						value: "印度尼西亚"
					},
					{
						text: "Iran",
						value: "伊朗"
					},
					{
						text: "Iraq",
						value: "伊拉克"
					},
					{
						text: "Ireland",
						value: "爱尔兰"
					},
					{
						text: "Israel",
						value: "以色列"
					},
					{
						text: "Italy",
						value: "意大利"
					},
					{
						text: "IvoryCoast",
						value: "科特迪瓦"
					},
					{
						text: "Jamaica",
						value: "牙买加"
					},
					{
						text: "Japan",
						value: "日本"
					},
					{
						text: "Jordan",
						value: "约旦"
					},
					{
						text: "Kazakhstan",
						value: "哈萨克斯坦"
					},
					{
						text: "Kenya",
						value: "肯尼亚"
					},
					{
						text: "Kiribati",
						value: "基尔巴斯"
					},
					{
						text: "Kuwait",
						value: "科威特"
					},
					{
						text: "Kyrgyzstan",
						value: "吉尔吉斯斯坦"
					},
					{
						text: "Laos",
						value: "老挝"
					},
					{
						text: "Latvia",
						value: "拉脱维亚"
					},
					{
						text: "Lebanon",
						value: "黎巴嫩"
					},
					{
						text: "Lesotho",
						value: "莱索托"
					},
					{
						text: "Liberia",
						value: "利比里亚"
					},
					{
						text: "Libya",
						value: "利比亚"
					},
					{
						text: "Liechtenstein",
						value: "列支敦士登"
					},
					{
						text: "Lithuania",
						value: "立陶宛"
					},
					{
						text: "Luxembourg",
						value: "卢森堡"
					},
					{
						text: "NorthMacedonia",
						value: "马其顿"
					},
					{
						text: "Madagascar",
						value: "马达加斯加"
					},
					{
						text: "Malawi",
						value: "马拉维"
					},
					{
						text: "Malaysia",
						value: "马来西亚"
					},
					{
						text: "Maldives",
						value: "马尔代夫"
					},
					{
						text: "Mali",
						value: "马里"
					},
					{
						text: "Malta",
						value: "马耳他"
					},
					{
						text: "MarshallIslands",
						value: "马绍尔群岛"
					},
					{
						text: "Mauritania",
						value: "毛里塔尼亚"
					},
					{
						text: "Mauritius",
						value: "毛里求斯"
					},
					{
						text: "Mexico",
						value: "墨西哥"
					},
					{
						text: "Micronesia",
						value: "密克罗尼西亚"
					},
					{
						text: "Moldova",
						value: "摩尔多瓦"
					},
					{
						text: "Monaco",
						value: "摩纳哥"
					},
					{
						text: "Mongolia",
						value: "蒙古"
					},
					{
						text: "Montenegro",
						value: "黑山"
					},
					{
						text: "Morocco",
						value: "摩洛哥"
					},
					{
						text: "Mozambique",
						value: "莫桑比克"
					},
					{
						text: "Myanmar",
						value: "缅甸"
					},
					{
						text: "Namibia",
						value: "纳米比亚"
					},
					{
						text: "Nauru",
						value: "瑙鲁"
					},
					{
						text: "Nepal",
						value: "尼泊尔"
					},
					{
						text: "Netherlands",
						value: "荷兰"
					},
					{
						text: "NewZealand",
						value: "新西兰"
					},
					{
						text: "Nicaragua",
						value: "尼加拉瓜"
					},
					{
						text: "Niger",
						value: "尼日尔"
					},
					{
						text: "Nigeria",
						value: "尼日利亚"
					},
					{
						text: "NorthKorea",
						value: "朝鲜"
					},
					{
						text: "Norway",
						value: "挪威"
					},
					{
						text: "Oman",
						value: "阿曼"
					},
					{
						text: "Pakistan",
						value: "巴基斯坦"
					},
					{
						text: "Palau",
						value: "帕劳"
					},
					{
						text: "Panama",
						value: "巴拿马"
					},
					{
						text: "PapuaNewGuinea",
						value: "巴布亚新几内亚"
					},
					{
						text: "Paraguay",
						value: "巴拉圭"
					},
					{
						text: "Peru",
						value: "秘鲁"
					},
					{
						text: "Philippines",
						value: "菲律宾"
					},
					{
						text: "Poland",
						value: "波兰"
					},
					{
						text: "Portugal",
						value: "葡萄牙"
					},
					{
						text: "Qatar",
						value: "卡塔尔"
					},
					{
						text: "Romania",
						value: "罗马尼亚"
					},
					{
						text: "Russia",
						value: "俄罗斯"
					},
					{
						text: "Rwanda",
						value: "卢旺达"
					},
					{
						text: "SaintKittsandNevis",
						value: "圣基茨和尼维斯"
					},
					{
						text: "SaintLucia",
						value: "圣卢西亚"
					},
					{
						text: "SaintVincentandtheGrenadines",
						value: "圣文森特和格林纳丁斯"
					},
					{
						text: "Samoa",
						value: "萨摩亚"
					},
					{
						text: "SanMarino",
						value: "圣马力诺"
					},
					{
						text: "SaoTomeandPrincipe",
						value: "圣多美和普林西比"
					},
					{
						text: "SaudiArabia",
						value: "沙特阿拉伯"
					},
					{
						text: "Senegal",
						value: "塞内加尔"
					},
					{
						text: "Serbia",
						value: "塞尔维亚"
					},
					{
						text: "Seychelles",
						value: "塞舌尔"
					},
					{
						text: "SierraLeone",
						value: "塞拉利昂"
					},
					{
						text: "Singapore",
						value: "新加坡"
					},
					{
						text: "Slovakia",
						value: "斯洛伐克"
					},
					{
						text: "Slovenia",
						value: "斯洛文尼亚"
					},
					{
						text: "SolomonIslands",
						value: "所罗门群岛"
					},
					{
						text: "Somalia",
						value: "索马里"
					},
					{
						text: "SouthAfrica",
						value: "南非"
					},
					{
						text: "SouthKorea",
						value: "南朝鲜"
					},
					{
						text: "SouthSudan",
						value: "南苏丹"
					},
					{
						text: "Spain",
						value: "西班牙"
					},
					{
						text: "SriLanka",
						value: "斯里兰卡"
					},
					{
						text: "Sudan",
						value: "苏丹"
					},
					{
						text: "Suriname",
						value: "苏里南"
					},
					{
						text: "Eswatini",
						value: "斯威士兰"
					},
					{
						text: "Sweden",
						value: "瑞典"
					},
					{
						text: "Switzerland",
						value: "瑞士"
					},
					{
						text: "Syria",
						value: "叙利亚"
					},
					{
						text: "Tajikistan",
						value: "塔吉克斯坦"
					},
					{
						text: "Tanzania",
						value: "坦桑尼亚"
					},
					{
						text: "Thailand",
						value: "泰国"
					},
					{
						text: "Togo",
						value: "多哥"
					},
					{
						text: "Tonga",
						value: "汤加"
					},
					{
						text: "TrinidadandTobago",
						value: "特立尼达和多巴哥"
					},
					{
						text: "Tunisia",
						value: "突尼斯"
					},
					{
						text: "Turkey",
						value: "土耳其"
					},
					{
						text: "Turkmenistan",
						value: "土库曼斯坦"
					},
					{
						text: "Tuvalu",
						value: "图瓦卢"
					},
					{
						text: "Uganda",
						value: "乌干达"
					},
					{
						text: "Ukraine",
						value: "乌克兰"
					},
					{
						text: "UnitedArabEmirates",
						value: "阿联酋"
					},
					{
						text: "UnitedKingdom",
						value: "英国"
					},
					{
						text: "UnitedStates",
						value: "美国"
					},
					{
						text: "Uruguay",
						value: "乌拉圭"
					},
					{
						text: "Uzbekistan",
						value: "乌兹别克斯坦"
					},
					{
						text: "Vanuatu",
						value: "瓦努阿图"
					},
					{
						text: "VaticanCity",
						value: "梵蒂冈"
					},
					{
						text: "Venezuela",
						value: "委内瑞拉"
					},
					{
						text: "Vietnam",
						value: "越南"
					},
					{
						text: "Yemen",
						value: "也门"
					},
					{
						text: "Zambia",
						value: "赞比亚"
					},
					{
						text: "Zimbabwe",
						value: "津巴布韦"
					}
				],

				valiFormData: {
					'candidate_name': '',
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
					url: '/subpkg/entryOtherInfo/entryOtherInfo'
				})
			},
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