<template>
	<view class="">
		<view class="portraitBox">
			<image src="../../static/bg.jpg" mode="" style="width: 100%" class="bg"></image>
			<view class="portrait" @click="goIn('ModifiedData/ModifiedData')">
				<image :src="date.avatar" mode=""></image>
				<text class="name_he juzhong">{{date.username}}</text>
			</view>
			<view class="vipBox">
				<view class="icon_vip">
					<image src="../../static/g.png" mode=""></image>
				</view>
				
				<!-- <svg t="1584520849157" class="icon_vip" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg"
				 p-id="3636" width="200" height="200">
					<path d="M495.274667 170.453333a21.333333 21.333333 0 0 1 33.450666 0L704.533333 392.533333a21.333333 21.333333 0 0 0 25.130667 6.368l171.392-73.450666a21.333333 21.333333 0 0 1 29.301333 23.946666l-94.912 457.28A85.333333 85.333333 0 0 1 751.893333 874.666667H272.106667a85.333333 85.333333 0 0 1-83.552-67.989334l-94.912-457.28a21.333333 21.333333 0 0 1 29.290666-23.946666l171.402667 73.450666a21.333333 21.333333 0 0 0 25.130667-6.368l175.808-222.08z"
					 p-id="3637" fill="#C94B01"></path>
				</svg> -->
				<text class="juzhong" style="left: 75upx;">会员积分1.99</text>
			</view>
		</view>
		<view class="myOrder" @click="goIn('Myorder/myorder')">
			<text>我的订单</text><text>全部订单</text>
			<view class="icon_sel juzhong">
				<image src="../../static/arrow_right.png" mode=""></image>
			</view>
		</view>
		<view class="btn">
			<view class="btnBox" v-for="(item,index) in btnMsg" :key="index" @click="goIn(item.url)">
				<image :src="item.img" mode="" class=""></image>
				<view class="">
					{{item.txt}}
				</view>
			</view>
		</view>
		<view class="cen">
			<image src="https://tangzhe123-com.oss-cn-shenzhen.aliyuncs.com/public/5d8833ed94392.png" mode=""></image>
		</view>
		<view class="select">
			<view class="selectBox" v-for="(item,index) in selectMsg" :key="index">
				<view class="img juzhong">
					<image :src="item.img" mode="" class=""></image>
				</view>
				<view class="">
					{{item.txt}}
				</view>
				<view class="icon_sel juzhong">
					<image src="../../static/arrow_right.png" mode=""></image>
				</view>
				
			</view>
		</view>
		<view class="">
			<view class="selectBox" @click="goIn('Install/install')">
				<view class="img juzhong">
					<image src="../../static/SJ.png" mode="" class=""></image>
				</view>
				<view class="">
					更多设置
				</view>
				<view class="icon_sel juzhong">
					<image src="../../static/arrow_right.png" mode=""></image>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				date: {
					avatar:"../../static/logo.png",
					username: "000"
				},
				name: '测试',
				btnMsg: [{
						img: '../../static/money.png',
						txt: '待付款',
						url: 'Myorder/myorder'
					},
					{
						img: '../../static/cart.png',
						txt: '待收货',
						url: 'Myorder/myorder'
					},
					{
						img: '../../static/PJ.png',
						txt: '待评价',
						url: 'Myorder/myorder'
					},
					{
						img: '../../static/BS.png',
						txt: '退换修',
						url: 'Myorder/myorder'
					}
				],
				selectMsg: [{
						img: '../../static/VIP.png',
						txt: '小米会员',
						url: ''
					},
					{
						img: '../../static/HG.png',
						txt: '会员中心',
						url: ''
					},
					{
						img: '../../static/X.png',
						txt: '服务中心',
						url: ''
					},
					{
						img: '../../static/home.png',
						txt: '小米之家',
						url: ''
					},
					{
						img: '../../static/next1.png',
						txt: '更多功能',
						url: ''
					}
				]
			}
		},
		created() {
			// 登录接口
			// let _this = this;
			// uni.request({
			// 	url: 'http://ceshi3.dishait.cn/api/login',
			// 	data: {
			// 		username: 'user2',
			// 		password: 'zcmcss'
			// 	},
			// 	method: 'POST',
			// 	success(e) {
			// 		console.log(e.data.data)
			// 		_this.date = e.data.data
			// 		// sessionStorage.setItem("use", e.data.data.token)
			// 		uni.setStorage({
			// 			key: 'use',
			// 			data: e.data.data.token
			// 		})
			// 		let str = uni.getStorage({
			// 			key: 'use'
			// 		})
					
			// 	}
			// })

		},
		methods: {
			goIn(e) {
				let use = uni.getStorage({
					key: 'user',
				});
				use.then(function(data){
					if(data.length==1){
						uni.navigateTo({
							url: '../Login/login'
						});
					}else{
						uni.navigateTo({
							url: '../' + e
						});
					}
				})
				console.log(use);
				
			}
		}
	}
</script>

<style scoped>
	.bg {
		width: 750upx;
		height: 352upx;
	}

	.portraitBox {
		height: 320upx;
		overflow: hidden;
		position: relative;
	}

	.portrait {
		position: absolute;
		top: 140upx;
		left: 90upx;
	}

	.portrait image {
		width: 130upx;
		height: 130upx;
		border-radius: 50%;
		overflow: hidden;
	}

	.juzhong {
		position: absolute;
		top: 50%;
		transform: translateY(-50%);
	}

	.name_he {
		width: 200upx;
		margin-left: 20upx;
		color: #fff;
	}

	.vipBox {
		color: #C94B01;
		width: 300upx;
		background-color: #FFD43F;
		font-size: 30upx;
		padding: 20upx 30upx;
		position: absolute;
		right: -30upx;
		top: 200upx;
		border-radius: 50upx 0 0 50upx;
	}

	.icon_vip {
		width: 30upx;
		height: 30upx;
		margin-left: 15upx;
	}

	.vipBox>text {
		margin-left: 10upx;
		line-height: 50upx;
	}

	.myOrder {
		height: 60upx;
		font-size: 36upx;
		line-height: 60upx;
		position: relative;
		padding: 25upx 40upx;
		border-bottom: 1px #ccc solid;
		font-weight: 600;
	}

	.myOrder text:nth-child(2) {
		font-size: 30upx;
		float: right;
		margin-right: 50upx;
		color: #666;
	}

	.icon_jt {
		width: 60upx;
		height: 60upx;
		right: 30upx;
	}

	.btn,
	.select {
		overflow: hidden;
		border-bottom: 13px solid rgba(170, 170, 170, .1);
	}

	.btnBox {
		width: 25%;
		text-align: center;
		float: left;
		font-size: 25upx;
		box-sizing: border-box;
		padding: 20upx 0;
		font-weight: 600;
		opacity: .7;
	}

	.btnBox image {
		width: 60upx;
		height: 60upx;
		opacity: .8;
	}

	.cen image {
		width: 750upx;
		height: 370upx;
	}

	.selectBox {
		position: relative;
		padding: 15px 100upx;
		border-bottom: 1px solid rgba(0, 0, 0, .1);
	}

	.selectBox .img {
		width: 40upx;
		height: 40upx;
		left: 40upx;
	}

	.selectBox image {
		width: 100%;
		height: 100%;
	}

	.icon_sel {
		width: 50upx;
		height: 50upx;
		right: 30upx;
	}
	
	.icon_sel>image{
		width: 100%;
		height: 100%;
	}
	.icon_vip>image{
		width: 100%;
		height: 100%;
	}
</style>
