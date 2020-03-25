<template>
	<view class="main">
		<view class="ma-top-1">
			<view class="ma-le">
				<view class="arce-1">
					<view class="arce-3">
						<image src="../../static/10.jpg" class="arrde"></image>
					</view>
				</view>
				<view class="arce-2">智能积木 越野四驱车</view>
			</view>
			<view class="ma-ri">
				<view class="opaci">
					<image src="../../static/timg.jpg" class="ha-1"></image>
				</view>
			</view>
		</view>
		<!-- 以上是导航栏搜索框部分 -->
		<view class="cen-arr-1">
			<view class="cen-ar-1">
				<view class="cen-ma-1 " v-bind:class="{'acuklje':arr==index}" v-for="(item,index) in arrde" :key="index" @click="goTop(index)">
					<view class="cen-ma-2">{{item.name}}</view>
				</view>
				<!--以上是滚动监听按钮-->
				<!--商品部分-->
			</view>
			<view class="cen-ar-2">

				<scroll-view scroll-y="true" class="arrde" @scroll="aacuege" :scroll-top="scrollTop">
					<view class="FGA" v-for="(item,index) in arrde" :key="index">
						<view class="ar-mak-1" v-for="(item,index) in item.app_category_items" :key="index" @click="goDetail">
							<view class="arrde kuget">
								<view class="haur">
									<image :src="item.cover" class="arrde"></image>
								</view>
								<view class="haur-oo-1">{{item.name}}</view>
							</view>
						</view>
					</view>
				</scroll-view>
			</view>
			<!--商品部分结束-->
			<!--如果数据过大，启用以下的遮照层，数据加载完成自动关闭-->
		</view>
		<view class="ma-kear-1" v-show="kacitueg">
			<view class="arrde-core">
				<image src="../../static/jz.gif" class="acre-opat"></image>
				<view class="kactu-ta">正在加载 请稍后</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				arrde: [], //滚动监听按钮以及商品数据
				kacitueg: true, //用于页面加载时判断遮照层是否显示
				arr: 0, //监听事件按钮
				// iocud:"",
				scollTopa: [0, 1],
				scrollTop: 0,
				old: {
					scrollTop: 0
				},
				upper: "",
				lower: ""
			}
		},
		onLoad: function(option) { //请求商品数据
			let _this = this
			uni.request({
				url: "http://ceshi3.dishait.cn/api/category/app_category",
				success: (res) => {
					// console.log(res.data.data)
					this.arrde = res.data.data //将商品数据赋值给变量
					let u_num = 0;
					let num = 0;
					for (let i = 0; i < res.data.data.length; i++) {
						let top = 0;
						console.log(res.data.data[i].app_category_items)
						num += res.data.data[i].app_category_items.length;
						console.log(num);
						_this.scollTopa[u_num+1] = parseInt(num * 250 / 3)
						u_num++;
					}
					// console.log(_this.scollTopa)
				}
			})

		},
		onReady: function() {

		},
		onShow: function() { //方法 数据初次渲染完成
			this.kacitueg = false //数据渲染完成时，将遮照层隐藏

		},

		methods: {
			aacuege(e) {
				this.old.scrollTop = e.detail.scrollTop
				// console.log(e.detail.scrollTop)
				if (this.old.scrollTop > 4390) {
					this.arr = 5
				} else if (this.old.scrollTop > 3500) {
					this.arr = 4
				} else if (this.old.scrollTop > 2640) {
					this.arr = 3
				} else if (this.old.scrollTop > 1700) {
					this.arr = 2
				} else if (this.old.scrollTop > 800) {
					this.arr = 1
				} else if (this.old.scrollTop > 100) {
					this.arr = 0
				}
			},
			goTop(e) {
				// console.log(this.scollTopa)
				let this_ = this;
				// this.scrollTop[0] = this.old.scrollTop;
				this.scrollTop = uni.upx2px(this_.scollTopa[e]);
				
				setTimeout(() => {
					this.arr = e;
				}, 100)
			},
			goDetail(){
				uni.navigateTo({
					url: "../detail/detail"
				})
			}
		}
	}
</script>

<style scoped>
	.main {
		width: 100%;
		height: 100%;
	}

	.ma-top-1 {
		width: 745upx;
		height: 100upx;
	}

	.ma-le {
		width: 630upx;
		height: 70upx;
		float: left;
		margin-top: 15upx;
		margin-left: 20upx;
		background-color: #F7F7F7;
		border-radius: 10upx;
	}

	.ma-ri {
		width: 80upx;
		height: 100upx;
		float: right;
	}

	.ha-1 {
		width: 100%;
		height: 100%;
		margin: auto;
	}

	.opaci {
		width: 50upx;
		height: 50upx;
		margin-top: 30upx;
		margin-left: 10upx;
	}

	.arce-1 {
		width: 80upx;
		height: 70upx;
		float: left;
	}

	.arce-2 {
		width: 500upx;
		line-height: 70upx;
		float: left;
		font-size: 30upx;
		text-indent: 30upx;
		color: #D5D5D5;
	}

	.arce-3 {
		width: 50upx;
		height: 50upx;
		margin-top: 10upx;
		margin-left: 20upx;
	}

	.arrde {
		width: 100%;
		height: 100%;
		float: left;
	}

	.cen-arr-1 {
		width: 745upx;
		height: 1100upx;
	}

	.cen-ar-1 {
		width: 200upx;
		height: 1000upx;
		float: left;
	}

	.cen-ar-1::after {
		clear: both;
		display: block;
		content: '';
	}

	.ar-mak-1::after {
		clear: both;
		display: block;
		content: '';
	}

	.cen-ar-2 {
		overflow: hidden;
		width: 490upx;
		height: 1100upx;
		float: left;
		margin-left: 25upx;
	}

	.cen-ma-1 {
		width: 200upx;
		height: 70upx;
		border-bottom: 1px solid #CCC;
		color: black;
		border-left: 3px solid white;
	}

	.cen-ma-2 {
		width: 200upx;
		line-height: 60upx;
		margin-top: 10upx;
		font-size: 30upx;
		text-align: center;
	}

	.ar-mak-1 {
		width: 140upx;
		height: 200upx;
		float: left;
		margin-left: 15upx;
		margin-top: 20upx;
		margin-bottom: 30upx;
	}

	.haur {
		width: 120upx;
		height: 130upx;
		margin: auto;
	}

	.haur-oo-1 {
		width: 135upx;
		line-height: 70upx;
		text-align: center;
		font-size: 30upx;
	}

	.ma-kear-1 {
		width: 100%;
		height: 100%;
		background-color: rgba(0, 0, 0, 0.9);
		position: absolute;
		top: 0;

	}

	.arrde-core {
		width: 300upx;
		height: 350upx;
		background-color: #191919;
		margin-left: 225upx;
		margin-top: 420upx;
	}

	.acre-opat {
		width: 100%;
		height: 300upx;
	}

	.kactu-ta {
		width: 100%;
		line-height: 40upx;
		color: #C8C7CC;
		text-align: center;
		font-size: 20upx;
	}

	.acuklje {
		color: #DEBD15;
		border-left: 3px solid #DEBD15;
	}

	.kuget {
		background-color: #F6F6F6;
	}

	.FGA::after {
		clear: both;
		display: block;
		content: '';
	}
</style>
