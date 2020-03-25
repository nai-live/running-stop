<template>
	<view class="body">
		<!-- 头部 -->
		<view class="top-cont">
			<view class="order-left">
				<view class="order-leftpicbox" @click="back">
					<image class="order-leftpic" src="../../static/search-pic2.png"></image>
				</view>
			</view>
			<view class="order-mille">
				<text class="mille-texe">我的订单</text>
			</view>
			<view class="order-right">
				<view class="order-picbox1">
					<image src="../../static/index-pic2.png"></image>
				</view>
				<view class="order-picbox2">
					<image src="../../static/cart-off.png"></image>
				</view>
			</view>
		</view>
		<!-- 导航栏-->
		<view class="bar">
			<block v-for="(item,index) in seear" :key="item.id">
				<view :data-id="index" class="con-text" @tap="setCurr" :class="{nnone:curr==index}">
					<text class="swiper-text">
						{{item}}
					</text>
				</view>
			</block>
		</view>
		<!-- 内容 -->
		<swiper class="content-box" :current="curr" @change="setCurr" :style="hig">
			<!-- 全部订单 -->
			<swiper-item class="swiper-box">
				<scroll-view scroll-y="true" style="height: 100%;">
					<view class="shop-box">
						<view class="details" v-for="(item,index) in order" :key="item.id">
							<view class="time-top">
								<text class="time">{{item.create_time}}</text>
								<text class="state">已收货</text>
							</view>
							<view class="details-middle">
								<view class="middle-one">
									<view class="middle-one-picbox">
										<image class="middle-one-pic" :src="item.order_items[0].goods_item.cover"></image>
									</view>
									<view class="middle-one-shop">
										<text class="shop-name">{{item.order_items[0].goods_item.title}}</text>
										<text class="shop-color">{{item.order_items[0].goods_skus.skus[0].value}}</text>
									</view>
									<view class="middle-two-shop">
										<text class="shop-price">￥{{item.order_items[0].price}}</text>
										<text class="shop-number">x{{item.order_items[0].num}}</text>
									</view>
								</view>
							</view>
							<view class="details-bottom">
								<view class="details-bottom-left"></view>
								<view class="details-bottom-right">
									<view class="bottom-right-allnum">
										<text class="bottom-right-text">共{{item.order_items[0].num}}件商品,合计:￥{{item.order_items[0].num*item.order_items[0].price}}</text>
									</view>
									<view class="bottom-right-btn">
										<text class="btn-one">查看物流</text>
										<text class="btn-two">确认收货</text>
									</view>
								</view>
							</view>
						</view>
						<view class="btn-s" @click="btns">查看更多</view>
					</view>
				</scroll-view>
			</swiper-item>
			<!-- 待付款 -->
			<swiper-item class="swiper-box">
				<scroll-view scroll-y="true" style="height: 100%;">
					<view class="shop-box">
						<view class="details" v-for="(item,index) in paid" :key="item.id">
							<view class="time-top">
								<text class="time">{{item.create_time}}</text>
								<text class="state">待付款</text>
							</view>
							<view class="details-middle">
								<view class="middle-one">
									<view class="middle-one-picbox">
										<image class="middle-one-pic" :src="item.order_items[0].goods_item.cover"></image>
									</view>
									<view class="middle-one-shop">
										<text class="shop-name">{{item.order_items[0].goods_item.title}}</text>
										<text class="shop-color">{{item.order_items[0].goods_skus.skus[0].value}}</text>
									</view>
									<view class="middle-two-shop">
										<text class="shop-price">￥{{item.order_items[0].price}}</text>
										<text class="shop-number">x{{item.order_items[0].num}}</text>
									</view>
								</view>
							</view>
							<view class="details-bottom">
								<view class="details-bottom-left"></view>
								<view class="details-bottom-right">
									<view class="bottom-right-allnum">
										<text class="bottom-right-text">共{{item.order_items[0].num}}件商品,合计:￥{{item.order_items[0].num*item.order_items[0].price}}</text>
									</view>
									<view class="bottom-right-btn">
										<text class="btn-one">查看物流</text>
										<text class="btn-two">确认收货</text>
									</view>
								</view>
							</view>
						</view>
						<view class="btn-s" @click="btns">查看更多</view>
					</view>
				</scroll-view>
			</swiper-item>
			<!-- 待收货 -->
			<swiper-item class="swiper-box">
				<scroll-view scroll-y="true" style="height: 100%;">
					<view class="shop-box">
						<view class="details" v-for="(item,index) in livery" :key="item.id">
							<view class="time-top">
								<text class="time">{{item.create_time}}</text>
								<text class="state">待收货</text>
							</view>
							<view class="details-middle">
								<view class="middle-one">
									<view class="middle-one-picbox">
										<image class="middle-one-pic" :src="item.order_items[0].goods_item.cover"></image>
									</view>
									<view class="middle-one-shop">
										<text class="shop-name">{{item.order_items[0].goods_item.title}}</text>
										<text class="shop-color">{{item.order_items[0].goods_skus.skus[0].value}}</text>
									</view>
									<view class="middle-two-shop">
										<text class="shop-price">￥{{item.order_items[0].price}}</text>
										<text class="shop-number">x{{item.order_items[0].num}}</text>
									</view>
								</view>
							</view>
							<view class="details-bottom">
								<view class="details-bottom-left"></view>
								<view class="details-bottom-right">
									<view class="bottom-right-allnum">
										<text class="bottom-right-text">共{{item.order_items[0].num}}件商品,合计:￥{{item.order_items[0].num*item.order_items[0].price}}</text>
									</view>
									<view class="bottom-right-btn">
										<text class="btn-one">查看物流</text>
										<text class="btn-two">确认收货</text>
									</view>
								</view>
							</view>
						</view>
						<view class="btn-s" @click="btns">查看更多</view>
					</view>
				</scroll-view>
			</swiper-item>
			<!-- 待评价 -->
			<swiper-item class="swiper-box">
				<scroll-view scroll-y="true" style="height: 100%;">
					<view class="shop-box">
						<view class="details" v-for="(item,index) in luate" :key="item.id">
							<view class="time-top">
								<text class="time">{{item.create_time}}</text>
								<text class="state">待评价</text>
							</view>
							<view class="details-middle">
								<view class="middle-one">
									<view class="middle-one-picbox">
										<image class="middle-one-pic" :src="item.order_items[0].goods_item.cover"></image>
									</view>
									<view class="middle-one-shop">
										<text class="shop-name">{{item.order_items[0].goods_item.title}}</text>
										<text class="shop-color">{{item.order_items[0].goods_skus.skus[0].value}}</text>
									</view>
									<view class="middle-two-shop">
										<text class="shop-price">￥{{item.order_items[0].price}}</text>
										<text class="shop-number">x{{item.order_items[0].num}}</text>
									</view>
								</view>
							</view>
							<view class="details-bottom">
								<view class="details-bottom-left"></view>
								<view class="details-bottom-right">
									<view class="bottom-right-allnum">
										<text class="bottom-right-text">共{{item.order_items[0].num}}件商品,合计:￥{{item.order_items[0].num*item.order_items[0].price}}</text>
									</view>
									<view class="bottom-right-btn">
										<text class="btn-one">查看物流</text>
										<text class="btn-two">确认收货</text>
									</view>
								</view>
							</view>
						</view>
						<view class="btn-s" @click="btns">查看更多</view>
					</view>
				</scroll-view>
			</swiper-item>
		</swiper>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				seear: ['全部', '待付款', '待收货', '待评价'], //导航栏文字数据
				curr: 0, //导航栏初始下标
				allorder: [], //全部订单
				unpaid: [], //待支付
				delivery: [], //待收货
				evaluate: [], //待评价
				hig: '', //屏幕的高度
				order: [], //全部订单渲染数据
				paid: [], //待支付渲染数据
				livery: [], //待收货渲染数据
				luate: [], //待评价渲染数据
				num: 10 //每次加载数据
			}
		},
		methods: {
			setCurr(e) { //切换轮播页面事件
				let thisCurr = e.detail.current || e.currentTarget.dataset.id || 0;
				this.curr = thisCurr;
			},
			back() { //返回
				uni.navigateBack({
					delta: 1
				})
			},
			btns() { //点击加载更多
				this.num += 10;
				this.order = this.allorder.slice(0, this.num)
				this.paid = this.unpaid.slice(0, this.num)
				this.livery = this.delivery.slice(0, this.num)
				this.luate = this.evaluate.slice(0, this.num)
				uni.showLoading({
					title: '加载中'
				});
				setTimeout(function() {
					uni.hideLoading();
				}, 500);
			}

		},
		onLoad() {
			let _that = this
			uni.getSystemInfo({ //获取屏幕高度
				success: function(res) {
					_that.hig = "height: " + (res.windowHeight - 100) + "px";
				}
			});
			let _this = this;

			let str = uni.getStorage({
				key: 'use'
			})
			//获取全部订单
			str.then(function(result) {
				uni.request({
					url: "http://ceshi3.dishait.cn/api/order/all",
					header: {
						'token': result[1].data
					},
					method: "POST",
					success(data) {
						_this.allorder = data.data.data
						_this.order = _this.allorder.slice(0, 10)
						console.log(_this.order)
					},
					fail(e) {
						console.log('报错')
					}
				})
			})
			//获取待付款
			str.then(function(result) {
				uni.request({
					url: "http://ceshi3.dishait.cn/api/order/paying",

					header: {
						'token': result[1].data
					},
					method: "POST",
					success(data) {
						_this.unpaid = data.data.data
					},
					fail(e) {
						console.log('报错')
					}
				})
			})
			//待收货
			str.then(function(result) {
				uni.request({
					url: "http://ceshi3.dishait.cn/api/order/receiving",

					header: {
						'token': result[1].data
					},
					method: "POST",
					success(data) {
						_this.delivery = data.data.data
					},
					fail(e) {
						console.log('报错')
					}
				})
			})
			// 待评价
			str.then(function(result) {
				uni.request({
					url: "http://ceshi3.dishait.cn/api/order/reviewing",

					header: {
						'token': result[1].data
					},
					method: "POST",
					success(data) {
						_this.evaluate = data.data.data
					},
					fail(e) {
						console.log('报错')
					}
				})
			})

		},
		onShow() {
			uni.showLoading({
				title: '正在加载'
			});
			setTimeout(function() {
				uni.hideLoading();
			}, 1000);
		}
	}
</script>

<style>
	.body {}

	.top-cont {
		width: 100%;
		height: 100upx;
		border-bottom: 1px solid #ccc;
	}

	.order-left {
		float: left;
		width: 10%;
		height: 100upx;
	}

	.order-mille {
		float: left;
		width: 70%;
		height: 100upx;
		text-align: center;
	}

	.order-right {
		float: left;
		width: 20%;
		height: 100upx;
	}

	.order-leftpicbox {
		width: 50upx;
		height: 50upx;
		margin: auto;
		margin-top: 25upx;
	}

	.order-leftpic {
		width: 100%;
		height: 100%;
		text-align: center;
	}

	.mille-texe {
		line-height: 100upx;
		font-weight: 500;
	}

	.order-picbox1 {
		width: 55upx;
		height: 55upx;
		display: inline-block;
		margin-top: 25upx;
		margin-right: 15upx;
	}

	.order-picbox2 {
		width: 55upx;
		height: 55upx;
		display: inline-block;
	}

	.order-right image {
		width: 100%;
		height: 100%;
	}

	/* 导航栏 */
	.bar {
		width: 100%;
		height: 90upx;
	}

	.con-text {
		line-height: 90upx;
		height: 90upx;
		width: 25%;
		float: left;
		text-align: center;
		font-size: 28upx;
		border-bottom: 4rpx solid white;
	}

	.nnone {
		line-height: 90upx;
		height: 90upx;
		width: 25%;
		float: left;
		text-align: center;
		font-size: 28upx;
		border-bottom: 4rpx solid #FD6801;
		color: #FD6801;
	}


	.swiper-box {
		background-color: #F5F5F5;
	}

	/* 全部订单 */
	.details {
		width: 100%;
		height: 450upx;
		background-color: white;
		margin-top: 20upx;
	}

	.time-top {
		width: 100%;
		height: 80upx;
		border-bottom: 2upx solid #ccc;
	}

	.time {
		width: 70%;
		height: 80upx;
		display: inline-block;
		line-height: 80upx;
		text-indent: 20upx;
		float: left;
		color: #BBBBBB;
		font-size: 26upx;
	}

	.state {
		width: 30%;
		height: 80upx;
		display: inline-block;
		line-height: 80upx;
		text-indent: 120upx;
		float: left;
		font-size: 24upx;
		color: #FD6801;
	}

	.details-middle {
		width: 100%;
		height: 190upx;
	}

	.middle-one {
		border-bottom: 2upx solid #ccc;
		width: 95%;
		height: 190upx;
		margin: auto;
	}

	.middle-one-picbox {
		width: 150upx;
		height: 150upx;
		margin-top: 18upx;
		margin-left: 20upx;
		float: left;
	}

	.middle-one-pic {
		width: 100%;
		height: 100%;
	}

	.middle-one-shop {
		width: 300upx;
		height: 190upx;
		float: left;
	}

	.shop-name {
		display: block;
		margin-top: 52upx;
		margin-bottom: 10upx;
		margin-left: 14upx;
		overflow: hidden;
		text-overflow: ellipsis;
		white-space: nowrap;
	}

	.shop-price {
		display: block;
		margin-top: 52upx;
		margin-bottom: 10upx;
		margin-left: 112upx;
		color: #B8B8B8;
		font-size: 30upx;
	}

	.shop-color {
		display: block;
		font-size: 26upx;
		color: #B8B8B8;
		margin-left: 14upx;
	}

	.shop-number {
		display: block;
		font-size: 26upx;
		color: #B8B8B8;
		margin-left: 14upx;
		text-indent: 160upx;
	}

	.middle-two-shop {
		width: 150upx;
		height: 190upx;
		float: left;
	}

	.details-bottom {
		width: 95%;
		height: 180upx;
		margin: auto;
	}

	.details-bottom-left {
		width: 50%;
		height: 180upx;
		float: left;
	}

	.details-bottom-right {
		width: 50%;
		height: 180upx;
		float: left;
	}

	.bottom-right-allnum {
		text-indent: 90upx;
		margin-top: 20upx;
	}

	.bottom-right-text {
		font-size: 26upx;
	}

	.btn-one,
	.btn-two {
		width: 150upx;
		height: 70upx;
		display: inline-block;
		border: 1px solid #B8B8B8;
		text-align: center;
		line-height: 70upx;
		font-size: 28upx;
		border-radius: 4upx;
		color: #999;
		margin-top: 30upx;
		margin-left: 20upx;
	}

	.btn-s {
		text-align: center;
	}
</style>
