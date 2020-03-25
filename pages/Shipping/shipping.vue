<template>
	<view id="main">
		<view class="mat-top">
			<!-- <view class="iocpug">购物车</view> -->
			<view class="ipcug" @click="mjacge">{{lakcu}}</view>
		</view>



		<view class="ardue">
			<view class="kacu-ra-1" v-for="(item,index) in date" :key="index" id="index">
				<view class="aocdu-icu-1">
					<view class="aitu-cig-1">
						<view class="ahd-ra-2" @click="cagrge(item)">
							<image :src="idue" class="viace"></image>
						</view>
					</view>
					<view class="aitu-cig-2">
						<view class="ahd-ra-1">
							<image :src="item.cover" class="viace"></image>
						</view>
					</view>
				</view>
				<view class="aocdu-icu-2">
					<view class="jach-iuc-1">{{item.title}}</view>
					<view class="jach-iuc-2">{{item.skusText}}</view>
					<view class="hactr" v-show="kcnueg" @click="ctarcyu(item.id)">
						<view class="tatc">{{item.skusText}}</view>
						<view class="cyat">
							<image src="../../static/xiala.png" class="kcger"></image>
						</view>
					</view>
					<view class="jach-iuc-3">
						<view class="jakc-opar-1">¥ <text class="icoer">{{item.pprice}}</text></view>
						<view class="jakc-opar-2">
							<view class="kajcha-1" @click="hacuge(item)">-</view>
							<view class="kajcha-2">{{item.num}}</view>
							<view class="kajcha-1" @click="haucarc(item)">+</view>
						</view>
					</view>
				</view>
			</view>
		</view>



		<view class="bacurad-opra-1" v-show="gecture">
			<view class="arduce">
				<view class="aico-ye-1">
					<image src="../../static/cart-off.png" class="viace"></image>
				</view>
				<view class="aico-ye-2">购物车还是空的</view>
				<view class="aico-ye-3">去逛逛</view>
			</view>
		</view>
		<view class="opkaci">
			<view class="kacj-ice-1">为你推荐</view>
			<view class="kacj-ice-2">
				<view class="ioc-jar-1"></view>
				<view class="ioc-jar-2">买了的人还买了</view>
				<view class="ioc-jar-1"></view>
			</view>
		</view>

		<view class="uiceyea">
			<view class="butt-ur" v-for="(item,index) in jcgure" :key="index">
				<view class="kacj-get-1">
					<image :src="item.cover" class="kcger"></image>
				</view>
				<view class="kacj-get-2">{{item.title}}</view>
				<view class="kacj-get-3">标配</view>
				<view class="kacj-get-4">¥<text class="arcdu-1">{{item.min_price}}</text><text class="arcdu-2">¥{{item.min_oprice}}</text></view>
			</view>
		</view>






		<view class="bottom">
			<view class="bu-op-1">
				<view class="kal-opa-1">
					<view class="konge" @click="icude">
						<image :src="idue" class="viace"></image>
					</view>
				</view>
				<view class="kal-opa-2">
					<view class="aicu-ir-1">合计:</view>
					<view class="aicu-ir-2">¥{{katce}}</view>
				</view>
			</view>
			<view class="bu-op-2">结算</view>
			<view class="aiue-kak-1" v-show="kcnueg">
				<view class="jacn-kya-1">移入收藏夹</view>
				<view class="jacn-kya-2">删除</view>
			</view>
		</view>

		<view class="tyrc" v-show="icudee">
			<view class="ty-to-1" @click="gcyy"></view>
			<view class="ty-bo-1">
				<view class="kacge-uig-1">
					<view class="yceic-1">
						<view class="jhcfg">
							<image :src="cayrd.cover" class="kcger"></image>
						</view>
					</view>
					<view class="yceic-2">
						<view class="lasyy-1">¥<text class="hayr">{{cayrd.min_price}}</text></view>
						<view class="lasyy-2">火焰红 64G 标配</view>
					</view>
				</view>
				<view class="acyra" v-for="(item,index) in msg" :key="index">
					<view class="gae-utg-1">{{index}}</view>
					<view class="gae-utg-2">
						<view class="tryc-rwc-1" :class="{'sdwyf':hcayr == data.skusText}" v-for="(item,index) in item" :key="index"
						 @click="cuary">{{item}}</view>
					</view>
				</view>
				<!-- <view class="gae-utg-3">容量</view>
				<view class="gae-utg-4">
					<view class="tryc-rwc-1">64GB</view>
					<view class="tryc-rwc-2">128GB</view>
				</view>
				<view class="gae-utg-5">配置</view>
				<view class="gae-utg-6">
					<view class="tryc-rwc-1">标配</view>
					<view class="tryc-rwc-2">套餐一</view>
					<view class="tryc-rwc-3">套餐二</view>
				</view> -->
				<view class="gae-utg-7"></view>
				<view class="gae-utg-8">
					<view class="ihct-le">购买数量</view>
					<view class="ihct-ri">
						<view class="gur-tcl-1" @click="dwyycw">-</view>
						<view class="gur-tcl-2">{{cuart}}</view>
						<view class="gur-tcl-3" @click="ucary">+</view>
					</view>
				</view>
				<view class="gae-utg-9">加入购物车</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				date: [], //购物车数据
				idue: "../../static/gou.png", //全选按钮
				kmaye: true, //全选按钮
				lakcu: "编辑", //编辑按钮
				kcnueg: false, //删除按钮
				gecture: false, //购物车为空时显示的
				jcgure: [], //购物车推荐列表
				icudee: false, //商品配置遮照层
				katce: 0.00, //总价格
				cuart: 1, //添加购物车数量
				msg: {}, //SKU数据
				cayrd: {}, //SKU配置的
				hcayr: '', //配置信息

			}
		},
		methods: {
			icude(e) { //全选按钮
				if (this.kmaye == true) {
					this.idue = "../../static/gou-red.png"
					this.kmaye = false
				} else {
					this.idue = "../../static/gou.png"
					this.kmaye = true
				}
			},
			gcyy: function() { //遮罩层
				this.icudee = false
			},
			haucarc: function(e) { //点击商品数量+1
				console.log(e)
				let _this = this;
				let car = e.id
				let vcer = e.num + 1
				e.num = e.num + 1
				let str = uni.getStorage({
					key: 'use'
				})

				str.then(function(result) { //获取购物车所有商品数据
					uni.request({
						url: "http://ceshi3.dishait.cn/api/cart/updatenumber/" + car + "",
						method: "POST",
						header: {
							'token': result[1].data
						},
						data: {
							num: vcer
						},
						success(data) {

						},
						fail(e) {
							console.log('报错')
						}
					})
				})
			},
			hacuge: function(e) { //点击商品数量-1
				let _this = this;
				let car = e.id
				let vcer = e.num - 1
				let str = uni.getStorage({
					key: 'use'
				})
				if (e.num == 1) {
					e.num = 1
				} else {
					e.num = e.num - 1
					str.then(function(result) { //获取购物车所有商品数据
						uni.request({
							url: "http://ceshi3.dishait.cn/api/cart/updatenumber/" + car + "",
							method: "POST",
							header: {
								'token': result[1].data
							},
							data: {
								num: vcer
							},
							success(data) {

							},
							fail(e) {
								console.log('报错')
							}
						})
					})
				}

			},
			mjacge() { //编辑按钮
				if (this.lakcu == "编辑") {
					this.lakcu = "完成"
					this.kcnueg = true
				} else {
					this.lakcu = "编辑"
					this.kcnueg = false
				}
			},
			ctarcyu(e) { //获取筛选数据

				let _this = this;
				let ctarvy = e
				let str = uni.getStorage({
					key: 'use'
				})

				str.then(function(result) {
					uni.request({
						url: "http://ceshi3.dishait.cn/api/cart/" + ctarvy + "/sku",
						header: {
							'token': result[1].data
						},
						data: {

						},
						success(data) {
							console.log(data.data.data)
							let msga = data.data.data.goods_skus_card;
							for (let i = 0; i < msga.length; i++) {
								let msgb = msga[i].goods_skus_card_value
								_this.msg[msga[i].goods_skus_card_value[0].name] = new Array();
								// console.log(_this.msg)
								for (let j = 0; j < msgb.length; j++) {
									_this.msg[msga[i].goods_skus_card_value[0].name].push(msga[i].goods_skus_card_value[j].value)
								}
							}
							_this.msg = _this.msg
							// console.log(_this.msg)
							_this.cayrd = data.data.data
						},
						fail(e) {
							console.log('报错')
						}
					})
				})



				_this.icudee = true
				_this.cuart = 1
			},


			cagrge(e) { //价格
				console.log(e)
				this.katce = e.pprice * e.num
			},

			ucary() { //筛选数量+1
				this.cuart = this.cuart + 1
			},

			dwyycw() { //筛选数量-1
				if (this.cuart == 1) {
					this.cuart = 1
				} else {
					this.cuart = this.cuart - 1
				}
			},

			cuary() {
				console.log(132)
			}



		},
		onLoad: function(option) {
			// uni.request({
			// 	url:"http://ceshi3.dishait.cn/api/cart",
			// 	msg:"ok",
			// 	header: {
			// 	        'token': 'ture' //自定义请求头信息
			// 	},
			// 	success: (res) => {
			// 		console.log(res)
			// 	}

			// })


			let _this = this;

			let str = uni.getStorage({
				key: 'use'
			})

			str.then(function(result) { //获取购物车所有商品数据
				if (result[1]) {
					_this.gecture = false
					uni.request({
						url: "http://ceshi3.dishait.cn/api/cart",
						header: {
							'token': result[1].data
						},
						success(data) {
							if (data.data.data.length == 0) {
								
							} else {
								
							}
							_this.date = data.data.data;
							// console.log(_this.date.skusText)

							_this.hcayr = data.data.data.skusText
							console.log(data.data.data.skusText)

						},
						fail(e) {
							console.log('报错')
						}
					})
				}else{
					_this.gecture = true
				}

			})


			uni.request({
				url: "http://ceshi3.dishait.cn/api/goods/hotlist",
				success: (res) => {

					_this.jcgure = res.data.data
				}
			})

		}


	}
</script>

<style scoped>
	#main {
		width: 745upx;
	}

	.bottom {
		width: 100%;
		height: 120upx;
		position: fixed;
		bottom: 0;
		border: 1px solid #CCC;
		background-color: white;
	}

	.bu-op-1 {
		width: 450upx;
		height: 120upx;
		float: left;
	}

	.bu-op-2 {
		width: 290upx;
		line-height: 120upx;
		background-color: #FD6801;
		float: right;
		text-align: center;
		color: white;
		font-size: 40upx;
	}

	.kal-opa-1 {
		width: 150upx;
		height: 120upx;
		float: left;
	}

	.kal-opa-2 {
		width: 290upx;
		height: 120upx;
		float: left;
	}

	.konge {
		width: 50upx;
		height: 50upx;
		margin-top: 35upx;
		margin-left: 50upx;
	}

	.aicu-ir-1 {
		width: 100upx;
		line-height: 120upx;
		float: left;
		font-size: 35upx;
		text-indent: 15upx;

	}

	.aicu-ir-2 {
		width: 180upx;
		line-height: 110upx;
		float: left;
		color: red;
		font-size: 35upx;
		text-indent: 10upx;
	}

	.viace {
		width: 100%;
		height: 100%;
	}

	.mat-top {
		width: 100%;
		line-height: 60px;
		overflow: hidden;
	}

	.ipcug {
		width: 100upx;
		line-height: 60px;
		float: right;
		text-align: center;
		font-size: 33upx;
	}

	.iocpug {
		width: 630upx;
		line-height: 60upx;
		float: left;
		text-indent: 300upx;
		font-size: 35upx;
	}

	.ardue {
		width: 100%;
		position: relative;
	}

	.bacurad-opra-1 {
		width: 100%;
		height: 180upx;
		padding-top: 30upx;
	}

	.arduce {
		width: 500upx;
		height: 150upx;
		margin: auto;
	}

	.aico-ye-1 {
		width: 80upx;
		height: 80upx;
		float: left;
		margin-left: 8upx;
		margin-top: 34upx;
	}

	.aico-ye-2 {
		width: 280upx;
		line-height: 150upx;
		color: #CCC;
		font-size: 35upx;
		float: left;
		text-indent: 10upx;
	}

	.aico-ye-3 {
		margin-top: 40upx;
		width: 110upx;
		line-height: 50upx;
		border: 2px solid #CCC;
		float: left;
		border-radius: 10upx;
		text-align: center;
		font-size: 30upx;
	}

	.opkaci {
		width: 100%;
		height: 140upx;
		background-color: #F5F5F5;
		padding-top: 50upx;
	}

	.kacj-ice-1 {
		width: 100%;
		line-height: 50upx;
		text-align: center;
		font-size: 35upx;
		color: #FD6801;
	}

	.kacj-ice-2 {
		width: 100%;
		height: 80upx;
	}

	.ioc-jar-1 {
		width: 245upx;
		height: 20upx;
		border-bottom: 1px solid #CCC;
		float: left;
		margin-top: 14upx;
	}

	.ioc-jar-2 {
		width: 250upx;
		line-height: 50upx;
		text-align: center;
		float: left;
		font-size: 30upx;
		margin-top: 10upx;
		color: #B8B8B8;
	}

	.kacu-ra-1 {
		width: 745upx;
		height: 300upx;
		border-top: 1px solid #CCC;
		border-bottom: 1px solid #CCC;
		position: relative;
	}

	.aocdu-icu-1 {
		width: 340upx;
		height: 100%;
		float: left;
	}

	.aocdu-icu-2 {
		width: 390upx;
		height: 100%;

		float: right;
	}

	.aitu-cig-1 {
		width: 100upx;
		height: 300upx;
		float: left;
	}

	.aitu-cig-2 {
		width: 230upx;
		height: 230upx;
		float: left;
		border: 1px solid #CCC;
		margin-top: 30upx;
	}

	.ahd-ra-1 {
		width: 190upx;
		height: 190upx;
		border: 1px solid #CCC;
		margin-top: 20upx;
		margin-left: 20upx;
	}

	.ahd-ra-2 {
		width: 50upx;
		height: 50upx;

		margin-left: 20upx;
		margin-top: 120upx;
	}

	.jach-iuc-1 {
		width: 100%;
		line-height: 60upx;
		font-size: 35upx;
		margin-top: 25upx;
	}

	.jach-iuc-2 {
		width: 100%;
		line-height: 50upx;
		font-size: 30upx;
		color: #838B93;
		margin-top: 20upx;
	}

	.jach-iuc-3 {
		width: 100%;
		height: 80upx;
		margin-top: 20upx;
	}

	.jakc-opar-1 {
		width: 160upx;
		height: 100%;
		float: left;
		font-size: 30upx;
		color: red;
	}

	.jakc-opar-2 {
		width: 213upx;
		height: 70upx;
		border: 1px solid #CCC;
		float: right;
	}

	.icoer {
		font-size: 35upx;
		color: red;
	}

	.kajcha-1 {
		width: 70upx;
		line-height: 70upx;
		background-color: #F8F8F8;
		color: black;
		float: left;
		font-size: 30upx;
		text-align: center;
	}

	.kajcha-2 {
		width: 70upx;
		line-height: 70upx;
		float: left;
		text-align: center;
		font-size: 30upx;
		border-left: 1px solid #CCC;
		border-right: 1px solid #CCC;
	}

	.aiue-kak-1 {
		width: 600upx;
		height: 100%;
		background-color: red;
		position: absolute;
		top: 0;
		right: 0;
	}

	.jacn-kya-1 {
		width: 298upx;
		line-height: 120upx;
		float: left;
		color: white;
		font-size: 40upx;
		text-align: center;
		background-color: #FD6801;
	}

	.jacn-kya-2 {
		width: 298upx;
		line-height: 120upx;
		float: right;
		background-color: red;
		color: white;
		font-size: 40upx;
		text-align: center;
	}

	.uiceyea {
		width: 100%;
		padding-bottom: 120upx;
		overflow: hidden
	}

	.butt-ur {
		width: 360upx;
		height: 550upx;
		float: left;
		margin-bottom: 10upx;
		margin-left: 10upx;
	}

	.kacj-get-1 {
		width: 100%;
		height: 350upx;
	}

	.kacj-get-2 {
		width: 100%;
		line-height: 60upx;
		font-size: 30upx;
		text-indent: 20upx;
	}

	.kacj-get-3 {
		width: 100%;
		line-height: 60upx;
		font-size: 35upx;
		color: #CCC;
		text-indent: 20upx;
	}

	.kacj-get-4 {
		width: 100%;
		line-height: 60upx;
		color: red;
		font-size: 30upx;
		text-indent: 20upx;
	}

	.arcdu-1 {
		font-size: 40upx;
	}

	.arcdu-2 {
		color: #666666;
		font-size: 28upx;
		text-decoration: line-through;
		margin-left: 20upx;
	}

	.kcger {
		width: 100%;
		height: 100%;
	}

	.tyrc {
		width: 100%;
		height: 100%;
		background-color: rgba(0, 0, 0, 0.5);
		position: fixed;
		top: 0;
	}

	.ty-to-1 {
		width: 100%;
		height: 200upx;
		padding-bottom: -20upx;
	}

	.ty-bo-1 {
		width: 100%;
		height: 1030upx;
		border: 1px solid white;
		border-top-left-radius: 30upx;
		border-top-right-radius: 30upx;
		background-color: white;
	}

	.kacge-uig-1 {
		width: 100%;
		height: 200upx;
		margin-top: 20upx;
	}

	.yceic-1 {
		width: 200upx;
		height: 200upx;
		border: 1px solid #CCC;
		margin-left: 20upx;
		float: left;
		margin-right: 30upx;
	}

	.yceic-2 {
		width: 400upx;
		height: 200upx;
		float: left;
	}

	.jhcfg {
		width: 180upx;
		height: 180upx;
		margin-top: 10upx;
		margin-left: 10upx;
	}

	.lasyy-1 {
		color: red;
		font-size: 30upx;
		margin-top: 40upx;
	}

	.lasyy-2 {
		font-size: 35upx;
		margin-top: 10upx;
		color: black;
	}

	.hayr {
		font-size: 40upx;
	}

	.gae-utg-1 {
		width: 100%;
		line-height: 60upx;
		font-size: 35upx;
		margin-top: 20upx;
		text-align: left;
		text-indent: 50upx;
	}

	.gae-utg-2 {
		width: 100%;
		height: 60upx;
		margin-top: 20upx;
	}

	.tryc-rwc-1 {
		width: 180upx;
		line-height: 60upx;
		text-align: center;
		font-size: 35upx;
		float: left;
		margin-left: 30upx;
		border-radius: 10upx;
		background-color: #F8F9FB;
	}

	.tryc-rwc-2 {
		width: 180upx;
		line-height: 60upx;
		text-align: center;
		font-size: 35upx;
		float: left;
		margin-left: 70upx;
		margin-right: 70upx;
		border-radius: 10upx;
		background-color: #F8F9FB;
	}

	.tryc-rwc-3 {
		float: left;
		width: 180upx;
		line-height: 60upx;
		font-size: 35upx;
		border-radius: 10upx;
		text-align: center;
		background-color: #F8F9FB;
	}

	.gae-utg-3 {
		width: 100%;
		line-height: 60upx;
		font-size: 40upx;
		margin-top: 15upx;
		text-indent: 50upx;
	}

	.gae-utg-4 {
		width: 100%;
		height: 80upx;
		margin-top: 15upx;
	}

	.gae-utg-5 {
		font-size: 40upx;
		width: 100%;
		line-height: 60upx;
		text-indent: 50upx;
		margin-top: 15upx;
	}

	.gae-utg-6 {
		width: 100%;
		height: 60upx;
		margin-top: 15upx;
	}

	.gae-utg-7 {
		width: 100%;
		height: 5upx;
		border-bottom: 1px solid #CCC;
		margin-top: 30upx;
	}

	.gae-utg-8 {
		width: 100%;
		height: 80upx;
		margin-top: 20upx;
	}

	.ihct-le {
		width: 200upx;
		line-height: 80upx;
		font-size: 30upx;
		float: left;
		text-indent: 30upx;
	}

	.ihct-ri {
		width: 300upx;
		height: 70upx;
		float: right;
		margin-top: 5upx;
	}

	.gur-tcl-1,
	.gur-tcl-3 {
		width: 70upx;
		line-height: 70upx;
		float: left;
		font-size: 40upx;
		background-color: #F8F8F8;
		text-align: center;
		border: 1px solid #CCC;
	}

	.gur-tcl-1 {
		border-top-left-radius: 8upx;
		border-bottom-left-radius: 8upx;
	}

	.gur-tcl-3 {
		border-top-right-radius: 8upx;
		border-bottom-right-radius: 8upx;
	}

	.gur-tcl-2 {
		width: 70upx;
		line-height: 70upx;
		float: left;
		border: 1px solid #CCC;
		text-align: center;
	}

	.gae-utg-9 {
		width: 100%;
		line-height: 110upx;
		background-color: #FD6801;
		font-size: 35upx;
		position: absolute;
		bottom: 0;
		text-align: center;
		color: white;
		margin-top: 20upx;
	}

	.hactr {
		width: 390upx;
		height: 60upx;
		position: absolute;
		top: 95upx;
		left: 355upx;
		background-color: #F1F1F1;
		text-indent: 10upx;
	}

	.tatc {
		line-height: 60upx;
		font-size: 30upx;
		float: left;
	}

	.cyat {
		width: 30upx;
		height: 30upx;
		float: right;
		margin-top: 17upx;
		margin-right: 40upx;
	}

	.acyra {
		width: 100%;
		height: 170upx;
	}

	.sdwyf {
		color: #FA8D44;
		background-color: #FCE0D5;
		border: 2px solid #F97F2A;
	}
</style>
