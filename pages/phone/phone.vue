<template>
	<view id="main">
		<view class="top">
			<view class="top-left">
				<image style="width: 50rpx; height: 50rpx; background-color: #eeeeee;" :src="img"></image>
			</view>
			<view class="top-right">
				忘记密码
			</view>
		</view>
		<view class="h1">
			手机号登录
		</view>
		<view class="from">
			<form @submit="formSubmit">
				<view class="">
					<input class="input" name="input" placeholder="请输入手机号" />
					<input class="inp" name="input" placeholder="请输入验证码" />
				</view>
				<view class="phone" @click="goLogin">用账号密码登录 ></view>
				<view class="bg">
					<button form-type="submit">登录</button>
				</view>
				<!-- <view class="">已阅读并同意小米账号协议、隐私政策和小米商城用户协议</view> -->
				<view class="check">
					<checkbox-group name="checkbox">
						<label>
							<checkbox class="checkbox" value="checkbox2" /><text>已阅读并同意小米账号协议、隐私政策和小米商城用户协议</text>
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
			}
		},
		onLoad() {

		},
		methods: {
			goLogin() {
				uni.navigateTo({
					url: "../Login/login"
				})
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
