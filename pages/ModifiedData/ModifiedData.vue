<template>
	<view class="body">
		<view class="box head">
			头像
			<view class="juzhong img">
				<image :src="date.avatar" mode=""></image>
			</view>
			
			
		</view>
		<view class="box">
			姓名<text class="name_he juzhong">{{date.username}}</text>
			<view class="icon_sel juzhong">
				<image src="../../static/arrow_right.png" mode=""></image>
			</view>
		</view>
		<view class="box">
			性别
			<view class="icon_sel juzhong">
				<image src="../../static/arrow_right.png" mode=""></image>
			</view>
		</view>
		<view class="box birthday">
			生日
			<view class="icon_sel juzhong">
				<image src="../../static/arrow_right.png" mode=""></image>
			</view>
		</view>
		<view class="box pass">
			修改密码
			<view class="icon_sel juzhong">
				<image src="../../static/arrow_right.png" mode=""></image>
			</view>
		</view>
		<view class="box">
			密保手机
			<view class="icon_sel juzhong">
				<image src="../../static/arrow_right.png" mode=""></image>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				date: {},
			}
		},
		methods: {

		},
		created() {
			let _this = this;
			uni.request({
				url: 'http://ceshi3.dishait.cn/api/login',
				data: {
					username: 'user2',
					password: 'zcmcss'
				},
				method: 'POST',
				success(e) {
					console.log(e.data.data)
					_this.date = e.data.data
				}
			});
		}
	}
</script>

<style scoped>
	page {
		background-color: #f8f8f8;
	}

	.juzhong {
		position: absolute;
		top: 50%;
		transform: translateY(-50%);
	}

	.box {
		border-bottom: 1px solid #f8f8f8;
		background-color: #fff;
		padding: 15px 40upx;
		position: relative;
	}

	.head {
		padding: 30px 40upx;
		border-top: 15px solid #f8f8f8;
	}

	.icon_sel {
		width: 50upx;
		height: 50upx;
		right: 30upx;
	}
	.img{
		width: 50px;
		height: 50px;
		right: 20upx;
		border-radius: 50%;
		overflow: hidden;
	}
	.img image{
		width: 100%;
		height: 100%;
	}
	.name_he{
		right: 80upx;
	}
	.birthday{
		
	}
	.pass{
		border-top: 15px solid #f8f8f8;
	}
	.icon_sel>image{
		width: 100%;
		height: 100%;
		opacity: .3;
	}
</style>
