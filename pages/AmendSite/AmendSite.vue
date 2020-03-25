<template>
	<view>
		<uni-nav-bar left-icon="back" left-text="返回" title="编辑收货地址" @clickLeft="titleLeft()" @clickRight="titleRight()">
			<view slot="right" v-show="id">
				删除
			</view>
		</uni-nav-bar>
		<view class="body">

			<view class="WTable" style="display: table;">
				<view class="WTr" style="display: table-row;">
					<view class="WTd" style="display: table-cell; text-align: right;">
						收货人：
					</view>
					<view class="WTd" style="display: table-cell;">
						<input type="text" :value="name" @input="inputName" />
					</view>
				</view>
				<view class="WTr" style="display: table-row;">
					<view class="WTd" style="display: table-cell;text-align: right;">
						手机号码：
					</view>
					<view class="WTd" style="display: table-cell;">
						<input type="text" :value="phone" @input="inputPhone" />
					</view>
				</view>
				<view class="WTr JG" style="display: table-row;">
					<view class="WTd" style="display: table-cell;">

					</view>
					<view class="WTd" style="display: table-cell;">

					</view>
				</view>
				<view class="WTr" style="display: table-row;">
					<view class="WTd" style="display: table-cell;text-align: right;">
						所在地区：
					</view>
					<view class="WTd" style="display: table-cell;">
						<input type="text" :value="province+city+district" @focus="show" />
					</view>
				</view>
				<view class="WTr" style="display: table-row;">
					<view class="WTd" style="display: table-cell;text-align: right;">
						详细地址：
					</view>
					<view class="WTd" style="display: table-cell;">
						<input type="text" :value="address" @input="inputAddress" />
					</view>
				</view>
				<view class="WTr JG" style="display: table-row;">
					<view class="WTd" style="display: table-cell;">

					</view>
					<view class="WTd" style="display: table-cell;">

					</view>
				</view>
				<view class="WTr" style="display: table-row;">
					<view class="WTd" style="display: table-cell;text-align: right;">
						设为默认地址：
					</view>
					<view class="WTd" style="display: table-cell; text-align: right;">
						<switch :checked="autoplay" @change="changeAutoplay" color="#FD6801" />
					</view>
				</view>
			</view>
			<view class="btnBox">
				<button type="primary" @click="submit">保存</button>
			</view>

			<view class="fiexd" :class="{'none':!Show}">
				<view class="option">
					<picker-view indicator-style="height: 50px;" style="width: 100%; height: 300px;" :value="value" @change="bindChange">
						<picker-view-column>
							<view v-for="(item,index) in provinces" :key="index" style="line-height: 50px">{{item}}</view>
						</picker-view-column>
						<picker-view-column>
							<view v-for="(item,index) in citys" :key="index" style="line-height: 50px">{{item}}</view>
						</picker-view-column>
						<picker-view-column>
							<view v-for="(item,index) in districts" :key="index" style="line-height: 50px">{{item}}</view>
						</picker-view-column>
					</picker-view>
				</view>
				<view class="fiexdBox">
					<button type="primary" @click="hide">确定</button>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import uniNavBar from "@/components/uni-nav-bar/uni-nav-bar.vue"

	const date = {
		'河北省': {
			'石家庄市': ['市辖区', '长安区', '桥东区', '桥西区', '新华区', '井陉矿区'],
			'唐山市': ['市辖区', '路南区', '路北区', '古冶区', '开平区', '丰南区'],
			'秦皇岛市': ['市辖区', '海港区', '山海关区', '北戴河区', '青龙满族自治县', '昌黎县'],
			'邯郸市': ['市辖区', '邯山区', '丛台区', '复兴区', '峰峰矿区', '邯郸县'],
			'邢台市': ['市辖区', '桥东区', '桥西区', '邢台县', '临城县', '内丘县']
		},
		'内蒙古': {
			'呼和浩特市': ['市辖区', '新城区', '回民区', '玉泉区', '赛罕区', '土默特左旗'],
			'包头市': ['市辖区', '东河区', '昆都仑区', '青山区', '石拐区', '白云矿区'],
			'乌海市': ['市辖区', '海勃湾区', '海南区', '乌达区']
		},
		'辽宁省': {
			'沈阳市': ['市辖区', '和平区', '沈河区', '大东区', '皇姑区', '铁西区'],
			'大连市': ['市辖区', '中山区', '西岗区', '沙河口区', '甘井子区', '金州区'],
			'鞍山市': ['市辖区', '铁东区', '铁西区', '立山区', '千山区', '台安县'],
			'抚顺市': ['市辖区', '新抚区', '东洲区', '望花区', '顺城区', '抚顺县'],
		},
		'吉林省': {
			'长春市': ['市辖区', '南关区', '宽城区', '朝阳区'],
			'吉林市': ['市辖区', '昌邑区', '龙潭区', '永吉县'],
			'四平市': ['市辖区', '铁西区', '铁东区', '梨树县']
		},
	}
	let province = new Array()
	for (let i in date) {
		province.push(i)
	}

	export default {
		data() {
			return {
				//date 获取到的用户地址数据
				date: [{
						id: 3,
						user_id: 3,
						province: "广东省",
						city: "广州市",
						district: "海珠区",
						address: "阅江西路232号",
						zip: 0,
						name: "帅哥",
						phone: "13564568789",
						last_used_time: 1568636040,
						create_time: "2019-08-13 16:19:05",
						update_time: "2019-09-16 20:14:00"
					},
					{
						id: 2,
						user_id: 3,
						province: "广东省",
						city: "广州市",
						district: "海珠区",
						address: "阅江西路222号广州塔",
						zip: 0,
						name: "靓仔",
						phone: "13564568789",
						last_used_time: null,
						create_time: "2019-08-13 16:19:03",
						update_time: "2019-08-13 16:19:03"
					}
				],
				id: false, //跳转过来的时候是否带id
				msgs: '', //默认值
				name: "", //名字
				phone: '', //电话
				address: '', //详细地址
				msg: {
					'河北省': {
						'石家庄市': ['市辖区', '长安区', '桥东区', '桥西区', '新华区', '井陉矿区'],
						'唐山市': ['市辖区', '路南区', '路北区', '古冶区', '开平区', '丰南区'],
						'秦皇岛市': ['市辖区', '海港区', '山海关区', '北戴河区', '青龙满族自治县', '昌黎县'],
						'邯郸市': ['市辖区', '邯山区', '丛台区', '复兴区', '峰峰矿区', '邯郸县'],
						'邢台市': ['市辖区', '桥东区', '桥西区', '邢台县', '临城县', '内丘县']
					},
					'内蒙古': {
						'呼和浩特市': ['市辖区', '新城区', '回民区', '玉泉区', '赛罕区', '土默特左旗'],
						'包头市': ['市辖区', '东河区', '昆都仑区', '青山区', '石拐区', '白云矿区'],
						'乌海市': ['市辖区', '海勃湾区', '海南区', '乌达区']
					},
					'辽宁省': {
						'沈阳市': ['市辖区', '和平区', '沈河区', '大东区', '皇姑区', '铁西区'],
						'大连市': ['市辖区', '中山区', '西岗区', '沙河口区', '甘井子区', '金州区'],
						'鞍山市': ['市辖区', '铁东区', '铁西区', '立山区', '千山区', '台安县'],
						'抚顺市': ['市辖区', '新抚区', '东洲区', '望花区', '顺城区', '抚顺县'],
					},
					'吉林省': {
						'长春市': ['市辖区', '南关区', '宽城区', '朝阳区'],
						'吉林市': ['市辖区', '昌邑区', '龙潭区', '永吉县'],
						'四平市': ['市辖区', '铁西区', '铁东区', '梨树县']
					},
				}, //省市区数据
				provinces: province, //省份数据
				citys: ['邢台市', '大连市'], //所在省份的城市数据
				districts: ['市辖区', '南关区', '宽城区'], //所在城市的区或县数据
				province: '', //选中的省
				city: '', //选中的市
				district: '', //选中的区
				value: [0, 0, 0], //上下滑动选择的value值
				autoplay: "", //开关按钮的值
				defa: false, //是否默认
				Show: false, //控制省市级联显示隐藏
			}
		},
		methods: {
			addCity(e) { //修改不用省的市区
				this.citys = []
				let ind = this.msg[this.provinces[this.value[0]]]; //获取所在省份的所有市
				for (let i in ind) {
					this.citys.push(i);
				}
			},
			addDistricts(e) {
				this.districts = []
				let ind = this.msg[this.provinces[this.value[0]]][this.citys[this.value[1]]]; //获取所在市的所有区或县
				// console.log(this.msg);
				if (ind.length) {
					for (let i = 0; i < ind.length; i++) {
						this.districts.push(ind[i]);
					}
				}

			},
			bindChange(e) {
				let _this = this;
				this.value = e.detail.value
				// const val = e.detail.value
				// console.log(this.data.provinces[val[0]])
				_this.province = this.provinces[this.value[0]];
				_this.city = this.citys[this.value[1]];
				_this.district = this.districts[this.value[2]];
				this.addCity();
				this.addDistricts();
			},
			showCity(e) {
				let _this = this;

				_this.province = this.provinces[this.value[0]];
				_this.city = this.citys[this.value[1]];
				_this.district = this.districts[this.value[2]];
			},
			inputName(e) {
				console.log(e)
				this.name = e.detail.value
			},
			inputPhone(e) {
				this.phone = e.detail.value
			},
			inputAddress(e) {
				this.address = e.detail.value
			},
			changeAutoplay(e) {
				console.log(e.detail.value);
				if (e.detail.value) {
					this.defa = 1;
				} else {
					this.defa = 0;
				}
				// this.defa = e.detail.value;
			},
			//提交事件
			submit() {
				let ura = "http://ceshi3.dishait.cn/api/useraddresses";
				let _this = this;
				let use = uni.getStorage({
					key: "use"
				})
				console.log(this.id)
				if (this.id) {
					console.log("调用了修改接口")
					let ura = "http://ceshi3.dishait.cn/api/useraddresses/" + this.id
				} else {
					console.log("调用了添加接口")
				}

				console.log(ura)
				use.then(function(data) {
					console.log(data)
					uni.request({
						url: ura,
						method: "POST",
						header: {
							'token': data[1].data
						},
						data: {
							province: _this.province,
							city: _this.city,
							district: _this.district,
							address: _this.address,
							zip: 0,
							name: _this.name,
							phone: _this.phone,
							default: _this.defa,
						},
						success(data) {
							console.log(data)
							uni.navigateBack({
								delta: 2
							});
						}
					})
				})
			},
			show() {
				console.log("显示");
				this.Show = true;
			},
			hide() {
				this.Show = false;
			},
			titleLeft() {
				uni.navigateBack({
					delta: 1
				});
			},
			titleRight() {
					console.log("调用了删除接口");
					let _this = this;
				let use = uni.getStorage({
					key: "use"
				})
				use.then(function(data) {
					console.log(data)
					uni.request({
						url: "http://ceshi3.dishait.cn/api/useraddresses/"+ _this.id,
						method: "DELETE",
						header: {
							'token': data[1].data
						},
						success(data) {
							console.log(data)
							uni.navigateBack({
								delta: 2
							});
						}
					})
				})
			},

		},
		onLoad(option) {
			let _this = this;
			uni.request({
				url: 'http://ceshi3.dishait.cn/api/login',
				data: {
					username: 'user2',
					password: 'zcmcss'
				},
				method: 'POST',
				success(e) {
					uni.setStorage({
						key: 'use',
						data: e.data.data.token
					})
					let str = uni.getStorage({
						key: 'use'
					})
					//获取用户所有地址信息
					str.then(function(result) {
						uni.request({
							url: "http://ceshi3.dishait.cn/api/useraddresses/1",
							header: {
								'token': result[1].data
							},
							success(data) {
								console.log(data)
								_this.date = data.data.data;
								if (option.index) {
									_this.id = _this.date[option.index].id;
									_this.msgs = _this.date[option.index];
									_this.province = _this.date[option.index].province;
									_this.city = _this.date[option.index].city;
									_this.district = _this.date[option.index].district;
									_this.address = _this.date[option.index].address;
									_this.name = _this.date[option.index].name;
									_this.phone = _this.date[option.index].phone;
								}
								_this.addCity();
								_this.addDistricts();
								_this.showCity();
							},
							fail(e) {
								console.log('报错')
							}
						})
					})
				}
			})

		},
		created() {

		}
	}
</script>

<style scoped>
	.fiexd {
		width: 100%;
		height: 100%;
		position: fixed;
		background-color: rgba(255, 255, 255, .8);
		z-index: 10;
		top: 0;
	}

	.option {
		text-align: center;
		position: absolute;
		bottom: 10%;
		height: 300px;
		width: 100%;
	}

	.fiexdBox {
		width: 100%;
		box-sizing: border-box;
		padding: 0 10%;
		position: absolute;
		bottom: 20upx;
	}

	.fiexdBox button {
		background-color: #FD6801;
	}

	.none {
		display: none;
	}

	.body {}

	.WTable {
		font-size: 30upx;
		padding-bottom: 20upx;
		margin: auto;
		width: 100%;
	}

	.WTd {
		padding: 20upx 10upx;
		border-bottom: 1px solid rgba(0, 0, 0, .1);
	}

	.WTr {}

	.JG {
		height: 6px;
		background-color: rgba(0, 0, 0, .1);
		opacity: .4;
	}

	.JG>.WTd {
		border-bottom: 0px;
	}

	.btnBox {
		width: 100%;
		box-sizing: border-box;
		padding: 10upx 10upx;
	}

	.btnBox button {
		background-color: #FD6801;
	}
</style>
