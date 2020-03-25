<template>
	<view>
		<uni-nav-bar left-icon="back" left-text="返回" title="地址列表" @clickLeft="titleLeft()" @clickRight="titleRight()">
			<view slot="right" style="font-size: 50upx;">
				+
			</view>
		</uni-nav-bar>
		<view class="box">
			<view class="message " v-for="(item,index) in date" :key="index" @click="modCity(index)">
				<view class="">
					<text style="font-size: 40upx; color: #FD6801; font-weight: 600;">{{item.name}}</text><text style="font-size: 28upx;">{{item.phone}}</text>
				</view>
				<view class="">
					<text style="font-size: 30upx;">{{item.province}} {{item.city}} {{item.district}}</text>
				</view>
				<view class="">
					<text style="font-size: 28upx;">{{item.address}}</text>
				</view>
				<view class="btn">
					<view class="icon">
						<image src="../../static/arrow_right.png" mode=""></image>
					</view>
					
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import uniNavBar from "@/components/uni-nav-bar/uni-nav-bar.vue"
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
				use: '',
				scollTop: [0, 1]
			}
		},
		methods: {
			titleLeft() {
				uni.navigateBack({
				    delta: 1
				});
			},
			titleRight() {
				uni.navigateTo({
					//多个参数用&拼接:url: '../comment/comment?id='+id'&name='+name
					url: '../AmendSite/AmendSite'
				});
			},
			modCity(data) {
				console.log(data)
				uni.navigateTo({
					//多个参数用&拼接:url: '../comment/comment?id='+id'&name='+name
					url: '../AmendSite/AmendSite?index=' + data


				});
			}
		},
		components: {
			uniNavBar
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
					// console.log(e.data.data.token)
					// sessionStorage.setItem("use", e.data.data.token)
					uni.setStorage({
						key: 'use',
						data: e.data.data.token
					})
					let str = uni.getStorage({
						key: 'use'
					})
					// console.log(str)

					//获取用户所有地址信息
					str.then(function(result) {
						// console.log(result[1].data);
						uni.request({
							url: "http://ceshi3.dishait.cn/api/useraddresses/1",
							header: {
								'token': result[1].data
							},
							success(data) {
								// console.log(data.data.data)
								_this.date = data.data.data
							},
							fail(e) {
								console.log('报错')
							}
						})
					})

				}
			})
			
		}
	}
</script>

<style scoped>
	.message {
		color: #666;
		line-height: 1.8;
		padding: 20upx 40upx;
		border-bottom: 1px solid rgba(0, 0, 0, .2);
		position: relative;
	}

	.message text {
		padding: 0 20upx;
	}

	.icon {
		width: 100upx;
		height: 100upx;
		position: absolute;
		top: 50%;
		right: 50upx;
		transform: translateY(-50%);
	}
	.icon>image{
		width: 100%;
		height: 100%;
		opacity: .3;
	}
</style>
