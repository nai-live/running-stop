<template>
	<view class="body">
		<view class="title">
			账号管理
		</view>
		<view class="content">
			<view class="conBox" v-for="(item,index) in msg.one" :key="index" @click="goIn(item.url)">
				{{item.txt}}
				
				<view class="icon_sel">
					<image src="../../static/arrow_right.png" mode=""></image>
				</view>
			</view>

		</view>
		<view class="title">
			关于
		</view>
		<view class="content">
			<view class="conBox" v-for="(item,index) in msg.two" :key="index" @click="goIn(item.url)">
				{{item.txt}}
				<view class="icon_sel">
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
				msg: {
					one: [{
							txt: '个人资料',
							url: 'ModifiedData/ModifiedData'
						},
						{
							txt: '收货地址',
							url: 'AddSite/AddSite'
						}
					],
					two: [{
							txt: '关于商城',
							url: 'paper/paper'
						},
						{
							txt: '意见反馈',
							url: ''
						},
						{
							txt: '协议规则',
							url: ''
						},
						{
							txt: '资质证件',
							url: ''
						},
						{
							txt: '用户协议',
							url: ''
						},
						{
							txt: '隐私策略',
							url: ''
						}
					]
				}
			}
		},
		methods: {
			goIn(e) {
				console.log(1)
				if(e){
					uni.navigateTo({
						url: "../"+e
					})
				}
			}
		}
	}
</script>

<style scoped>
	page {
		background-color: #EEEEEE;
	}

	.body {}

	.title {
		padding: 15px 20upx;
		background-color: #EEEEEE;
	}

	.conBox {
		background-color: #fff;
		padding: 13px 40upx;
		border-bottom: 1px solid #EEEEEE;
		position: relative;
	}

	.icon_sel {
		position: absolute;
		top: 50%;
		transform: translateY(-50%);
		width: 50upx;
		height: 50upx;
		right: 30upx;
	}
	.icon_sel>image{
		width: 100%;
		height: 100%;
		opacity: .3;
	}
</style>

