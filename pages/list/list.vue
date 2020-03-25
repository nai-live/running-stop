<template>
	<view class="">
		<view class="option">
		</view>
		
		<view class="option">
			<view class="" v-for="(item,index) in opti" :key="index" @click="tizi(index)">
				<text :class="{'or':item.into}">{{item.msg}}</text>
				<view class="inTop" :class="{'GTop':item.into&&item.prog}">
				</view>
				<view class="inBottom" :class="{'GBottom':item.into&&!item.prog}">
				</view>
			</view>
			<view class="" @click="hide">
				<text class="or">筛选</text>
			</view>
		</view>
		<view class="list">
			<!-- <view v-for="(item,index) in msg" :key="index" class="listCon"> -->
			<view v-for="(item,index) in msg" :key="index" @click="goStore(item)" class="listCon">
				<image :src="item.cover" class="img"></image>
				<view class="text" :style="{width: halfWidth}">
					<view>
						{{item.title}}
					</view>
					<view>
						雅致简约/分体式入耳/收纳盒充电/蓝牙5.0/触控操作
					</view>
					<view>
						￥199
					</view>
					<view>
						1348条评论98%满意
					</view>
				</view>
			</view>

			<!-- </view> -->
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				opti: [ //按钮数据  intu为true时为选中状态  prog为true时为递增
					{
						msg: "综合",
						into: true,
						prog: true
					},
					{
						msg: "销量",
						into: false,
						prog: true
					},
					{
						msg: "价格",
						into: false,
						prog: true
					}
				],
				qingqiu: {
					key: '',
					value: ''
				},
				//列表数据
				msg: {}
			}
		},
		props: ["title"],
		methods: {
			tizi(e) {
				// console.log(uni.getSystemInfoSync())
				if (this.opti[e].into) {
					this.opti[e].prog = !this.opti[e].prog
				} else {
					for (let i = 0; i < this.opti.length; i++) {
						this.opti[i].into = false;
						this.opti[i].prog = true;
					}
					this.opti[e].into = true
					// console.log(this.opti)
				}
				let _this = this;
				if (this.opti[e].prog) {
					this.qingqiu.value = "desc"
				} else {
					this.qingqiu.value = "asc"
				}
				switch (e) {

					case 0:
						this.qingqiu.key = "all";
						uni.request({
							url: "http://ceshi3.dishait.cn/api/goods/search",
							method: "POST",
							data: {
								title: _this.title,
								page: 1,
								all: _this.qingqiu.value
							},
							success(res) {
								console.log(res.data.data)
								_this.msg = res.data.data;
							}
						})
						break;

					case 1:
						this.qingqiu.key = "sale_count";
						uni.request({
							url: "http://ceshi3.dishait.cn/api/goods/search",
							method: "POST",
							data: {
								title: _this.title,
								page: 1,
								sale_count: _this.qingqiu.value
							},
							success(res) {
								console.log(res.data.data)
								_this.msg = res.data.data;
							}
						})
						break;

					case 2:
						this.qingqiu.key = "min_price";
						uni.request({
							url: "http://ceshi3.dishait.cn/api/goods/search",
							method: "POST",
							data: {
								title: _this.title,
								page: 1,
								min_price: _this.qingqiu.value
							},
							success(res) {
								console.log(res.data.data)
								_this.msg = res.data.data;
							}
						})
						break;

					default:

				}



			},
			goStore(e) {
				console.log(e)
			},
			newMsg() {

			},
			hide() {
				this.$emit("getHide", true)
			}
		},
		computed: {
			halfWidth() {
				return uni.upx2px(750 - 300) + 'px';
			}

		},
		components: {

		},
		onReady() {
			let _this = this;
			// uni.request({
			// 	url: "http://ceshi3.dishait.cn/api/category/app_category",
			// 	success(res) {
			// 		console.log(res.data.data, _this.msg)
			// 		_this.msg = res.data.data;
			// 	}
			// })
			this.tizi(0);
			console.log(_this.title )
			// uni.request({
			// 	url: "http://ceshi3.dishait.cn/api/goods/search",
			// 	method: "POST",
			// 	data: {
			// 		title: _this.title,
			// 		page: 1,
			// 		all: "desc"
			// 	},
			// 	success(res) {
			// 		console.log(res.data.data)
			// 		_this.msg = res.data.data;
			// 	}
			// })
			// uni.request({
			//     url: 'http://ceshi3.dishait.cn/api/goods/search',
			//     data: {
			//         title: '小米',
			//         page: 3,
			// 		price: 5
			//     },
			//     header: {
			//         'custom-header': 'hello' //自定义请求头信息
			//     },
			//     success: function (res) {
			//         console.log(res.data);
			//     }
			// });
		},
		watch:{
			title(){
				this.tizi(0);
			}
		}
	}
</script>

<style scoped>
	.option {
		width: 100%;
		line-height: 1.8;
		color: #999;
		font-size: 40upx;
		text-align: center;
	}

	.option::after {
		clear: both;
		display: block;
		content: '';
	}

	.option>view {
		float: left;
		width: 25%;
		position: relative;
		border-top: #eee 1px solid;
		border-bottom: #eee 1px solid;
	}

	.inTop {
		width: 0;
		border: transparent 10upx solid;
		border-bottom: #ccc 10upx solid;
		position: absolute;
		top: 50%;
		transform: translateY(-50%);
		margin-top: -13upx;
		left: 50%;
		margin-left: 60upx;
	}

	.inBottom {
		width: 0;
		border: transparent 10upx solid;
		border-top: #ccc 10upx solid;
		position: absolute;
		top: 50%;
		transform: translateY(-50%);
		margin-top: 13upx;
		left: 50%;
		margin-left: 60upx;
	}

	.GTop {
		border-bottom: #FD6801 10upx solid;
	}

	.GBottom {
		border-top: #FD6801 10upx solid;
	}

	.or {
		color: #FD6801;
	}

	.listCon {
		position: relative;
		border-bottom: #eee solid 1px;
	}

	.listCon::after {
		clear: both;
		display: block;
		content: '';
	}

	.img {
		width: 300upx;
		height: 300upx;
	}

	image {
		box-sizing: border-box;
		padding: 30upx;
	}

	.text {
		box-sizing: border-box;
		padding: 20upx;
		position: absolute;
		top: 50%;
		transform: translateY(-50%);
		left: 300upx;
	}

	.img,
	.text {
		float: left;
	}

	.text>view {
		color: #999;
		font-size: 20upx;
		padding: 7upx 0;
	}

	.text view:nth-child(1) {
		color: #333;
		font-size: 35upx;
		font-weight: 700;
	}

	.text view:nth-child(3) {
		color: #FD6801;
		font-size: 30upx;
	}
</style>
