<template>
	<view id="main">
		<view class="top">
			<view class="top-left">
				<image style="width: 50rpx; height: 50rpx; background-color: #eeeeee;" :src="img" @click="goBack"></image>
			</view>
			<view class="top-right">
				忘记密码
			</view>
		</view>
		<view class="h1">
			密码登录
		</view>
		<view class="from">
			<form @submit="formSubmit">
				<view class="">
					<input class="input" name="user" placeholder="请输入手机号/邮箱/小米账号" @input="userChange"/>
					<input class="inp" type="password" name="password" placeholder="请输入密码" @input="passwordChange" />
				</view>
				<view class="phone" @click="goPhone">用手机短信登录 ></view>
				<view class="bg">
					<button form-type="submit">登录</button>
				</view>
				<!-- <view class="">已阅读并同意小米账号协议、隐私政策和小米商城用户协议</view> -->
				<view class="check">
					<checkbox-group name="checkbox" @change="chan($event)">
						<label>
							<checkbox class="checkbox" value="checkbox2"/><text>已阅读并同意小米账号协议、隐私政策和小米商城用户协议</text>
						</label>
					</checkbox-group>
				</view>

			</form>
		</view>
		<view class="login">
			<image style="width: 40rpx; height: 40rpx; background-color: #eeeeee;" :src="weibo"></image>
			<image style="width: 40rpx; height: 40rpx; background-color: #eeeeee;" :src="weixin"></image>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello',
				img: '../../static/six.png', //图片
				weibo: '../../static/weibo.png', //微博logo
				weixin: '../../static/weixin.png', //微信logo
				user: '',//用户名
				password: '',//密码
				look: false,//是否同意协议
			}
		},
		onLoad() {

		},
		methods: {
			goPhone() {
				uni.navigateTo({
					url: "../phone/phone"
				})
			},
			formSubmit(){
				// console.log("提交")
				let _this = this;
				if(this.look){
					console.log("勾选了",_this.user,_this.password)
					uni.request({
						url: 'http://ceshi3.dishait.cn/api/login',
						data: {
							username: _this.user,
							password: _this.password
						},
						method: 'POST',
						success(e) {
							console.log(e.data.data)
							if(e.data.data){
								_this.date = e.data.data
								// sessionStorage.setItem("use", e.data.data.token)
								uni.setStorage({
									key: 'use',
									data: e.data.data.token
								})
								uni.setStorage({
									key: 'user',
									data: e.data.data
								})
								uni.reLaunch({
									url: "../Index/index"
								})
								let str = uni.getStorage({
									key: 'use'
								})
							}
							
							
						},
						fail(e) {
							console.log("账号密码错误")
						}
					})
				}
			},
			goBack(){
				uni.navigateBack({
					delta:5
				})
			},
			userChange(e){
				this.user = e.detail.value;
				// console.log(this.user);
			},
			passwordChange(e){
				this.password = e.detail.value;
				// console.log(this.password);
			},
			chan(e){
				// console.log(e.detail.value[0])
				if(e.detail.value[0]){
					this.look = true;
				}else{
					this.look = false;
				}
			}
		}
	}
</script>

<style>
	page {
		width: 100%;
		height: 100%;
	}

	#main {
		width: 100%;
		height: 100%;
		background-color: #EEEEEE;
	}

	input {
		padding: 40rpx 0;
	}

	.input {
		border-bottom: 1px solid #EAD5BB;
	}

	.phone {
		margin: 50rpx 0;
		color: #666;
		font-size: 25rpx;
	}

	.inp {
		border-bottom: 1px solid #ccc;
	}

	.check {
		/* line-height: 25rpx; */
		font-size: 25rpx;
		color: #C0C0C0;
	}

	.bg {
		padding: 50rpx 0;
	}

	.bg button {
		background-color: #FFD8B9;
		color: white;
	}

	.top {
		width: 100%;
		height: 80rpx;
		line-height: 80rpx;
		background-color: #EEEEEE;
	}

	.top-left {
		width: 75%;
		line-height: 80rpx;
		/* height: 100%; */
		padding-left: 20rpx;
		float: left;
	}

	.top-left image {
		vertical-align: middle;
	}

	.top-right {
		width: 22%;
		height: 100%;
		float: right;
		color: #666;
		font-size: 32rpx;
	}

	.h1 {
		font-size: 44rpx;
		font-weight: bold;
		margin: 50rpx;
	}

	.from {
		padding: 50rpx;
	}

	.checkbox {
		width: 25rpx;
		height: 25rpx;
	}

	.login {
		width: 32%;
		margin: auto;
		padding-top: 50rpx;
	}

	.login image {
		margin-left: 50rpx;
	}
</style>
