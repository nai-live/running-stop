<template>
	<view id="main">
		<view class="top">
			<view class="top-left">
				<image @click="changeback" style="width: 50rpx; height: 50rpx; background-color: #eeeeee;" :src="img"></image>
				<text>小米商城</text>
			</view>
			<view class="top-right">
				<image style="width: 50rpx; height: 50rpx; background-color: #eeeeee;" :src="png"></image>
			</view>
		</view>
		<view class="p">
			Redmi K20 Pro常见购机咨询
		</view>
		<view class="refer">
			<view class="strong">
				售前咨询:
			</view>
			<view class="issue">
				<text>1.怎么参与Redmi K20 Pro订金预售？</text>
				<view>{{sale}}</view>
			</view>
			<!-- 2 -->
			<view class="issue">
				<text>2.订金预售的订金可以退换吗？</text>
				<view> 答: {{back}}</view>
			</view>
			<!-- 3 -->
			<view class="issue">
				<text>3.Redmi K20 Pro标配什么充电器？</text>
				<view> 答: {{charge}}</view>
			</view>
			<!-- 4 -->
			<view class="issue">
				<text>4.Redmi K20 Pro有哪些套装可以购买？</text>
				<view>答: 在售套装有:</view>
				<view>{{buyback}}</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello',
				img: '../../static/back.png', //图片
				png: '../../static/shop.png', //图片
				sale: '订金预售活动在5月28日10:00开启，成功支付订金后即表示成功预订Redmi K20 Pro手机。点击“我的” - “代付款” 即可进行尾款支付，尾款支付时间在6月1日0点至24点。',
				back: '支付100元订金后，还可以申请退款，退款将在财务审核后及时退回',
				charge: '原装标配18W充电器。Redmi K20 Pro最高可支持27W有线快充，如有需要，可自行选购。',
				buyback: 'Redmi K20 Pro + Redmi 20寸红色旅行箱套装。旅行箱原价299元，套装内现价价格199元，还在等什么，现在快来抢购吧！'
			}
		},
		onLoad() {

		},
		methods: {
			changeback(){
				uni.navigateBack({
					delta:1
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
	}

	.top {
		width: 100%;
		height: 80rpx;
		line-height: 80rpx;
		background-color: #EEEEEE;
		border-bottom: 1px solid #ccc;
	}

	.top image {
		vertical-align: middle;
	}

	.top image:first-child {
		margin: 0 35rpx;
	}

	.top-left {
		width: 80%;
		height: 100%;
		float: left;
		color: #666666;
		/* background-color: #4CD964; */
		/* padding: 0 35rpx; */
	}

	.top-right {
		width: 15%;
		height: 100%;
		float: right;
		/* background-color: #007AFF; */
		text-align: center;
	}

	.p {
		padding-left: 35rpx;
		font-size: 44rpx;
		/* margin: 50rpx 0; */
		margin-top: 50rpx;
	}

	.refer {
		width: 90%;
		height: auto;
		padding: 38rpx;
		background-color: #FFFFFF;
		line-height: 52rpx;
		font-size: 32rpx;
		/* color: ; */
		color: #474747;
	}

	.strong {
		font-weight: 900;
		font-size: 36rpx;
		margin-bottom: 10rpx;
	}
	
	.issue{
		margin-bottom: 28rpx;
	}
</style>
