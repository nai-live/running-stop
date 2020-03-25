<template>
	<view>
		
		<view class="box" v-for="(item,index) in msg" :key="index">
			<view class="leftBox">
				<view class="">
					<image src="../../static/region.png" mode=""></image>
				</view>
			</view>
			<view class="rightBox">
				<view class="name">
					{{item.name}}
				</view>
				<view class="phone">
					{{item.phone}}
				</view>
				<view class="">
					{{item.province}} - {{item.city}} - {{item.district}}
				</view>
				<view class="">
					{{item.address}}   {{item.zip}}
				</view>
			</view>
			
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				msg: [{
					address: "通天塔啊",
					city: "太原市",
					create_time: "1970-01-01 08:32:50",
					district: "小店区",
					id: 89,
					last_used_time: 1584887172,
					name: "头条",
					phone: "15910000000",
					province: "山西省",
					update_time: "2020-03-22 22:26:12",
					user_id: 3,
					zip: 0,
				}]
			}
		},
		methods: {

		},
		onLoad() {
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
								console.log(data.data.data)
								// _this.date = data.data.data
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
	.box {
		overflow: hidden;
	}
	.rightBox{
		width: 80%;
		float: left;
		font-size: 35upx;
	}
	.rightBox>view{
		padding: 10upx 10upx;
		overflow: hidden;
		text-overflow: ellipsis;
		white-space: nowrap;
	}
	.leftBox{
		width: 20%;
		float: left;
		position: relative;
		min-height: 10upx;
	}
	.leftBox>view{
		position: absolute;
		left: 50%;
		transform: translate(-50%, 50%);
		
	}
	.leftBox image{
		width: 75upx;
		height: 75upx;
	}
	.name{
		font-size: 45upx;
		color: #FD6801;
		font-weight: 600;
		
	}
	.phone{
		font-size: 35upx;
		color: #666;
	}
</style>
