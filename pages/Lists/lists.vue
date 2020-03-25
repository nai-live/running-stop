<template>
	<view>
		<view class="bar">
			<block v-for="(item,index) in menu" :key="item.id">
				<view :data-id="index" class="con-text" @tap="setCurr" :class="{nnone:curr==index}">
					<text class="swiper-text">
						{{item}}
					</text>
				</view>
			</block>
		</view>

		<swiper class="content-box" :current="curr" @change="setCurr">
			<swiper-item>
				<scroll-view>
					<view class="text-box">
						<view class="pic-box">
							<image class="pic" src="../../static/123.jpg"></image>
						</view>
						<view class="btn-box">
							<view class="left-box">
								<view class="txt-top">Redmi K20 Pro</view>
								<view class="txt-bottom">纹龙885 旗舰处理器</view>
							</view>
							<view class="right-box">
								<view class="btn">去购买</view>
							</view>
						</view>
						<view class="bottom-box">了解更多  ></view>
					</view>
					<view class="text-box">
						<view class="pic-box">
							<image class="pic" src="../../static/123.jpg"></image>
						</view>
						<view class="btn-box">
							<view class="left-box">
								<view class="txt-top">Redmi K20 Pro</view>
								<view class="txt-bottom">纹龙885 旗舰处理器</view>
							</view>
							<view class="right-box">
								<view class="btn">去购买</view>
							</view>
						</view>
						<view class="bottom-box">了解更多  ></view>
					</view>
				</scroll-view>
			</swiper-item>
			<swiper-item>
				<scroll-view>
					<view class="text-box">
						<view class="pic-box">
							<image class="pic" src="../../static/123.jpg"></image>
						</view>
						<view class="btn-box">
							<view class="left-box">
								<view class="txt-top">Redmi K20 Pro</view>
								<view class="txt-bottom">纹龙885 旗舰处理器</view>
							</view>
							<view class="right-box">
								<view class="btn">去购买</view>
							</view>
						</view>
						<view class="bottom-box">了解更多  ></view>
					</view>
					<view class="text-box">
						<view class="pic-box">
							<image class="pic" src="../../static/123.jpg"></image>
						</view>
						<view class="btn-box">
							<view class="left-box">
								<view class="txt-top">Redmi K20 Pro</view>
								<view class="txt-bottom">纹龙885 旗舰处理器</view>
							</view>
							<view class="right-box">
								<view class="btn">去购买</view>
							</view>
						</view>
						<view class="bottom-box">了解更多  ></view>
					</view>
				</scroll-view>
			</swiper-item>
			<swiper-item>
				<scroll-view>
					即将开售
				</scroll-view>
			</swiper-item>
			<swiper-item>
				<scroll-view>
					新品手机
				</scroll-view>
			</swiper-item>
		</swiper>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				menu: ['最热新品', '最近上新', '即将开售', '新品手机'],		//导航栏文字数据
				curr: 0,				//导航栏初始下标
				index: ''
			}
		},
		methods:{
			setCurr(e) {			//轮播页面点击事件
				let thisCurr = e.detail.current || e.currentTarget.dataset.id || 0;
				this.curr = thisCurr;
			}
		}
	}
</script>

<style>
	.bar {
		width: 100%;
		height: 70upx;
		border-bottom: 1px solid #ccc;
	}
	.content-box{
		width: 100%;
		height: 1100upx;
	}
	.con-text {
		line-height: 70upx;
		height: 70upx;
		width: 25%;
		float: left;
		text-align: center;
		font-size: 28upx;
		border-bottom: 2rpx solid white;
	}
	.nnone {
		line-height: 70upx;
		height: 70upx;
		width: 25%;
		float: left;
		text-align: center;
		font-size: 28upx;
		border-bottom: 2px solid #FD6801;
		color: #FD6801;
	}
	.text-box{
		width: 95%;	
		height: 470upx;
		margin: auto;
		margin-top: 30upx;
		border-radius: 7px;
		border: 1px solid #ccc;
		box-shadow:0px 4px 2px #eee;
		margin-bottom: 50upx;
	}
	.pic-box{
		width: 100%;
		height: 240upx;
		border-radius: 7px;
	}
	.pic{
		width: 100%;
		height: 100%;
		border-radius: 7px;
	}
	.btn-box{
		width: 100%;
		height: 130upx;
		border-bottom: 1px solid #ccc;
	}
	.left-box{
		float: left;
		width: 50%;
		height: 110upx;
		padding-top: 15upx;
	}
	.right-box{
		float: left;
		width: 48%;
		height: 110upx;
	}
	.txt-top{
		margin-bottom: 10upx;
		text-indent: 15upx;
	}
	.txt-bottom{
		text-indent: 15upx;
		color: #999;
		font-size: 26upx;
	}
	.btn{
		width: 120upx;
		height: 60upx;
		background-color: #FD6801;
		border-radius: 30px;
		color: white;
		text-align: center;
		margin: auto;
		line-height: 60upx;
		margin-top: 26upx;
		font-size: 26upx;
		margin-right: 0upx;
	}
	
	.bottom-box{
		width: 100%;
		height: 100upx;
		line-height: 100upx;
		text-align: center;
	}
</style>
