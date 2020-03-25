<template>
	<view id="main">
		<!-- 详情 -->
		<view class="nav">
			<view class="top">
				<view class="top-nav">
					<swiper class="swiper" :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval" :duration="duration">
						<swiper-item v-for="item in topimg">
							<image :src="item" style="width: 100%; height: 100%;"></image>
						</swiper-item>
					</swiper>
				</view>
				<view class="top-be" v-for="item in top">
					<view class="be-big">{{item.name}}</view>
					<text class="be-color">{{item.title}}</text>
					<view class="yellow">
						{{item.price}}
					</view>
				</view>
				<!-- 结束 -->
			</view>
			<view class="content">
				<view class="content-top">
					<scroll-view class="scroll-x" scroll-x="true" style="width: 100%;">
						<view class="cpu" v-for="item in nucleus">
							<image style="width: 50rpx; height: 50rpx; background-color: #FFFFFF;" :src="cpu"></image>
							<view>{{item.name}}</view>
							<text class="ccc">{{item.value}}</text>
						</view>
					</scroll-view>
				</view>
				<view class="content-nav">
					<view class="nav-one" @click="changebar">
						<view class="nav-a">
							已选
						</view>
						<view class="nav-b">

						</view>
						<view class="nav-c">
							<image style="width: 50rpx; height: 50rpx; background-color: #F5F5F3;" :src="next"></image>
						</view>
					</view>
					<!-- 2 -->
					<view class="nav-one" @click="changesite">
						<view class="nav-a">
							配送
						</view>
						<view class="nav-b">

						</view>
						<view class="nav-c">
							<image style="width: 50rpx; height: 50rpx; background-color: #F5F5F3;" :src="next"></image>
						</view>
					</view>
					<!-- 3 -->
					<view class="nav-the" @click="changeran">
						<view style="width: 90%; height: 100%; display: flex; justify-content: space-around; align-items: center; font-size: 30rpx;">
							<image style="width: 30rpx; height: 30rpx; background-color: #eeeeee;" :src="qte"></image>
							小米自营
							<image style="width: 30rpx; height: 30rpx; background-color: #eeeeee;" :src="qte"></image>
							小米发货
							<image style="width: 30rpx; height: 30rpx; background-color: #eeeeee;" :src="qte"></image>
							七天无理由退货
						</view>
						<view style="width: 10%; height: 100%; text-align: right;">
							<image style="width: 50rpx; height: 50rpx; background-color: #F5F5F3;" :src="next"></image>
						</view>
					</view>
				</view>
				<!-- 评论 -->
				<view class="review">
					<scroll-view class="scroll-x" scroll-x="true" style="width: 100%; height: 100%;">
						<view class="review-nav" v-for="item in review">
							<view class="review-top">
								<view style="width: 20%;">
									<image style="width: 80rpx; height: 80rpx; background-color: #eeeeee;" :src="item.user.avatar"></image>
								</view>
								<view style="width: 60%;">
									<view style="font-weight: 700;">{{item.user.nickname}}</view>
									<text style="color: #666; font-size: 26rpx;">{{item.review_time}}</text>
								</view>
								<view style="width: 20%;">
									<image style="width: 50rpx; height: 50rpx; background-color: #eeeeee;" :src="good"></image>
									<text style="color: #666; font-size: 26rpx;">{{item.id}}</text>
								</view>
							</view>
							<!-- 上半部分结束 -->
							<view class="review-der">
								<view style="margin-bottom: 20rpx; font-weight: 700;">{{item.review.data}}</view>
								<image :src="item.review.image[0]"></image>
							</view>
							<!-- 下半部分结束 -->
						</view>
					</scroll-view>
				</view>
				<view class="asd">
					<text>更多评论 > </text>
				</view>
				<!-- 大图开始 -->
				<view class="php">
					<view class="php-nav" v-for="item in php">
						<image :src="item"></image>
					</view>
				</view>
				<!-- <view class="php" v-html="php.content"></view> -->
				<!-- 大图结束 -->
				<view class="asd">
					<text> 为你推荐 </text>
				</view>
				<view class="recom">
					<view class="recom-nav" v-for="item in recom">
						<image style="width: 100%; height: 254rpx;" :src="item.cover"></image>
						<text style="font-size: 28rpx; font-weight: 700;">{{item.title}}</text>
						<view class="txt">{{item.desc}}</view>
						<view class="red">¥ {{item.min_price}} <text> ¥ {{item.min_oprice}}</text></view>
					</view>
				</view>
				<view class="dd">
					<text class="dd-nav">没 有 更 多 了 哦 ~ </text>
				</view>
			</view>

		</view>
		<!-- <view class="top-left">
			<image style="width: 50rpx; height: 50rpx; background-color: #ccc; border-radius: 50%;" :src="jpg"></image>
		</view>
		<view class="top-right">
			<image style="width: 50rpx; height: 50rpx; background-color: #ccc; border-radius: 50%;" :src="svg"></image>
		</view> -->

		<view class="bg" v-if="rig" @click="changeran">
			<!-- 第三层阴影 -->
		</view>
		<view class="bar" :class="{'ac' : rig==true}">
			<!-- 遮罩层一开始不显示 即true为this.rig的false-->
			<view class="bar-top">
				<text>服务说明</text>
			</view>
			<view class="bar-nav">
				<view>
					<image :src="qte" style="padding-right: 10rpx; width: 35rpx; height: 35rpx; vertical-align: middle;"></image>
					仿米自营
				</view>
				<view>
					<image :src="qte" style="padding-right: 10rpx; width: 35rpx; height: 35rpx; vertical-align: middle;"></image>
					仿米发货
					<!-- <view>1111111</view> -->
				</view>
				<text class="gray">由仿米发货</text>
				<view>
					<image :src="qte" style="padding-right: 10rpx; width: 35rpx; height: 35rpx; vertical-align: middle;"></image>
					7天无理由就是不退货
				</view>
				<view>
					<image :src="qte" style="padding-right: 10rpx; width: 35rpx; height: 35rpx; vertical-align: middle;"></image>
					运货说明
				</view>
				<view style="margin: 0px; color: gray; padding-left: 40rpx;">不管运费多少,就是不包邮</view>
				<text class="gray">特殊产品,也是一样</text>
			</view>
			<view id="bar-der" @click="changeran">
				确定
			</view>
			<!-- 结束 -->
		</view>
		<!-- 第三层结束 -->
		<view class="ag" v-if="cen" @click="changesite">
			<!-- 第二层阴影 -->
		</view>
		<view class="bar" :class="{'ac' : cen==true}">
			<view class="bar-top">
				<text>收货地址</text>
			</view>
			<view class="in-be">
				<image :src="site" style="width: 35rpx; height: 35rpx; padding-left: 20rpx;"></image>
				<text>
					<!-- 1111111111 --></text>
			</view>
			<view class="in-below">
				选择新的地址
			</view>
		</view>
		<!-- 第二层结束 -->
		<view class="cg" v-if="lef" @click="changebar">
			<!-- 第一层阴影 -->
		</view>
		<view class="bar" :class="{'ac' : lef==true}">
			<view class="be-top">
				<view class="be-left">
					<image src="../../static/8848phone.jpg" style="width: 80%; height: 80%; margin: auto;"></image>
				</view>
				<view class="be-right">
					<view class="be-in-right">
						<view class="yellow">¥8848</view>
						<text class="be-color">火焰红 64GB 标配</text>
					</view>
				</view>
			</view>
			<view class="be-nav">
				<view class="old">颜色</view>
				<view class="be-list">
					<view class="be-ing" :class="[index==id ? 'creeper' : '']" v-for="(item,index) in color" @click="changeadd(index)">
						<view style="width: 100%; height: 100%;">{{item}}</view>
					</view>
				</view>
				<!-- 2 -->
				<view class="old">容量</view>
				<view class="be-list" style="justify-content: flex-start;">
					<view class="be-ing" :class="[index==ic ? 'creeper' : '']" v-for="(item,index) in save" @click="changeasd(index)"
					 style=" margin-right: 60upx;">
						<view style="width: 100%; height: 100%;">{{item}}</view>
					</view>
				</view>
				<!-- 3 -->
				<view class="old">套餐</view>
				<view class="be-list">
					<view class="be-ing" :class="[index==ig ? 'creeper' : '']" v-for="(item,index) in meal" @click="changeabc(index)">
						<view style="width: 100%; height: 100%;">{{item}}</view>
					</view>
				</view>
				<!-- 结束 -->
			</view>
			<view class="btn">
				<view class="buy">
					购买数量
				</view>
				<view class="opx">
					<view class="opx-a" @click="del">
						-
					</view>
					<view class="opx-b">
						{{mag}}
					</view>
					<view class="opx-c" @click="add">
						+
					</view>
				</view>
			</view>
			<view class="be-shop" @click="changeshop">
				加入购物车
			</view>
		</view>
		<!-- 底部开始 -->
		<view class="below">
			<view class="below-left">
				<view class="cang">
					<image style="width: 50rpx; height: 50rpx; background-color: #eeeeee;" :src="img"></image>
					<view>收藏</view>
				</view>
				<view class="shop">
					<image style="width: 50rpx; height: 50rpx; background-color: #eeeeee;" :src="png"></image>
					<view>购物车</view>
				</view>
			</view>
			<view class="below-right" @click="changepdd">
				加入购物车
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				id: 0, //初始值
				ic: 0,
				ig: 0,
				mag: 1,
				rig: false, //条件
				cen: false,
				lef: false,
				title: 'Hello',
				peach: '../../static/8848phone.jpg', //图片
				site: '../../static/site.png',
				next: '../../static/next.png', //图片
				good: '../../static/good.png',
				qte: '../../static/true.png', //图片
				img: '../../static/like.png',
				png: '../../static/shop.png', //图片
				jpg: '../../static/return.png',
				svg: '../../static/more.png',
				cpu: '../../static/CPU.png', //图片
				nucleus: [], //CPU数据
				review: [], //评论数据
				recom: [], //为你推荐
				php: ['../../static/detail_1.png', '../../static/detail_2.png',
					'../../static/detail_3.png', '../../static/detail_4.png',
					'../../static/detail_5.png', '../../static/detail_6.png'
				], //大图
				topimg: ['../../static/tamg.jpg', '../../static/timg.jpg'], //轮播图
				top: [{
					// img: '../../static/tamg.jpg', 轮播图下面的数据
					name: '小米MIX3 6GB+128GB',
					title: '磁动力滑盖全面屏 / 前后旗舰AI双摄 / 四曲面彩色陶瓷机身 / 高效10W无线充电',
					price: "¥3298"
				}],
				// 选项
				color: ['火焰红', '炭黑', '冰川兰'],
				save: ['64GB', '128GB'],
				meal: ['标配', '套餐一', '套餐二'],

				// 轮播数据
				indicatorDots: true,
				vertical: false,
				autoplay: true,
				interval: 2000,
				duration: 500
			}
		},
		onLoad(option) {
			//cpu数据
			uni.request({
					url: 'http://ceshi3.dishait.cn/api/goods/25',
					success: (res) => {
						//console.log(res.data.data.content); //所有图片
						// this.php = res.data.data
						this.nucleus = res.data.data.goodsAttrs //.splice(0,3)
					}
				}),
				//评论数据
				uni.request({
					url: 'http://ceshi3.dishait.cn/api/goods/25/comments/good?page=1',
					success: (res) => {
						console.log(res.data.data);
						this.review = res.data.data.list;
					}
				}),
				//为你推荐
				uni.request({
					url: 'http://ceshi3.dishait.cn/api/goods/hotlist',
					success: (res) => {
						// console.log(res.data.data);
						this.recom = res.data.data;
					}
				})
		},
		methods: {
			changepdd: function(e) {
				uni.showToast({
				    title: '请选择规格',
				    duration: 2000
				});
				this.lef = !this.lef;
			},
			changeshop: function(e) {
				uni.showToast({
				    title: '加入成功!',
				    duration: 2000
				});
				this.lef = !this.lef;
			},
			changesite: function(e) {
				// console.log('picker发送选择改变，携带值为', e.target.value)
				this.cen = !this.cen;
			},
			changeran: function(e) {
				// console.log(e.target.id)
				this.rig = !this.rig;
			},
			changebar: function(e) {
				this.lef = !this.lef;
			},
			changeadd: function(index) {
				// console.log(index);
				this.id = index;
				// id: e.target.id;
			},
			changeasd: function(index) {
				this.ic = index;
			},
			changeabc: function(index) {
				this.ig = index;
			},
			add: function() {
				this.mag = this.mag + 1;
			},
			del: function() {
				this.mag = this.mag - 1;
				if (this.mag <= 0) {
					this.lef = !this.lef;
					this.mag = 1;
				}
			}
		}
	}
</script>

<style>
	.creeper {
		color: #EF995A;
		background-color: #FCE0D5 !important;
	}

	.old {
		margin-top: 10upx;
	}

	.top-be {
		width: 97%;
		line-height: 52upx;
		padding-left: 20upx;
	}

	.be-big {
		font-size: 40upx;
		font-weight: bold;
	}

	.be-color {
		font-size: 26upx;
		color: #666;
	}

	.yellow {
		font-size: 40upx;
		color: #F26C0F;
	}

	.ac {
		bottom: 0upx !important;
		transition-duration: 0.8s;
	}

	page {
		width: 100%;
		height: 100%;
	}

	#main {
		width: 100%;
		height: 100%;
	}

	.nav {
		width: 100%;
		height: 4888px;
		position: relative;
		/* background-color: #3F536E; */
	}

	.top {
		width: 100%;
		height: 716upx;
		background-color: #EEEEEE;
	}

	.top-left {
		width: 50rpx;
		height: 50rpx;
		position: fixed;
		top: 0;
		left: 0;
	}

	.top-right {
		width: 50rpx;
		height: 50rpx;
		position: fixed;
		top: 0;
		right: 0;
	}

	.content {
		width: 94.5%;
		padding: 20rpx;
		height: 94.93%;
	}

	.below {
		width: 100%;
		/* height: 8%; */
		height: 96.46rpx;
		clear: both;
		position: fixed;
		bottom: 0;
	}

	.below-left {
		float: left;
		width: 50%;
		height: 100%;
		background-color: #EEEEEE;
	}

	.below-right {
		float: right;
		width: 50%;
		height: 100%;
		background-color: #FD6801;
		line-height: 96.46rpx;
		text-align: center;
		color: white;
	}

	.cang {
		width: 50%;
		height: 100%;
		float: left;
		/* background-color: #4CD964; */
		text-align: center;
		font-size: 30rpx;
		color: #666;
		/* background-size: 12px auto; */
		/* background: url(../../static/like.png) 0px 0px no-repeat; */
	}

	.shop {
		width: 50%;
		height: 100%;
		float: right;
		/* background-color: #007AFF; */
		text-align: center;
		font-size: 30rpx;
		color: #666;
		/* background-size: 50rpx 50rpx; */
		/* background: url(../../static/shop.png) 0px 0px no-repeat; */
	}

	.cpu {
		width: 150rpx;
		height: 146rpx;
		/* white-space: nowrap; */
		display: inline-block;
		margin-right: 44rpx;
		text-align: center;
		line-height: 44rpx;
	}

	.scroll-x {
		white-space: nowrap;
	}

	.ccc {
		color: #B2B2B2;
		font-size: 26rpx;
	}

	.content-top {
		width: 100%;
		height: 146rpx;
	}

	.content-nav {
		width: 95%;
		height: 300rpx;
		background-color: #F5F5F3;
		padding: 20rpx;
		margin: 20rpx 0;
	}

	.nav-one {
		width: 100%;
		height: 80rpx;
		color: #666666;
		line-height: 80rpx;
		border-bottom: 1px solid #CCCCCC;
		margin-bottom: 20rpx;
	}

	.nav-the {
		width: 100%;
		height: 80rpx;
		color: #666666;
		line-height: 80rpx;
		border-bottom: 1px solid #CCCCCC;
		display: flex;
		/* background-color: #4CD964; */
	}

	.nav-the>view>image {
		vertical-align: middle;
	}

	.nav-one>view {
		float: left;
	}

	.nav-one>view:first-child {
		text-align: center;
		width: 20%;
		height: 100%;
		/* background-color: #3F536E; */
	}

	.nav-one>view:nth-child(2) {
		width: 60%;
		height: 100%;
		/* background-color: #474747; */
	}

	.nav-one>view:last-child {
		text-align: right;
		width: 20%;
		height: 100%;
		/* background-color: #4CD964; */
	}

	.nav-one>view:last-child image {
		vertical-align: middle;
		/* line-height: 80rpx; */
	}

	.review {
		width: 95%;
		height: 420rpx;
		/* background-color: #F5F5F3; */
		/* padding: 20rpx; */
	}

	.review-nav {
		width: 80%;
		height: 100%;
		background-color: #EEEEEE;
		font-size: 30rpx;
		padding: 10rpx;
		margin: 10rpx;
		display: inline-block;
	}

	.review-top {
		width: 100%;
		height: 30%;
		/* background-color: #3F536E; */
		display: flex;
		flex-direction: row;
		align-items: center;
	}

	.review-top image {
		vertical-align: middle;
	}

	.review-der>view {
		width: 100%;
		height: 25%;
	}

	.review-der>image {
		width: 100%;
		height: 260upx;
		vertical-align: middle;
		margin: auto;
	}

	.review-der {
		width: 100%;
		height: 70%;
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
	}

	.asd {
		width: 100%;
		height: 80rpx;
		line-height: 80rpx;
		text-align: center;
		color: #007AFE;
		margin: 20rpx 0;
		font-weight: bold;
		font-size: 34rpx;
	}

	.recom {
		width: 100%;
		height: 1260rpx;
		/* background-color: #FFD8B9; */
		display: flex;
		flex-wrap: wrap;
		flex-direction: row;
	}

	.recom-nav {
		width: 47%;
		height: 400rpx;
		line-height: 44rpx;
		margin: 10rpx;
		background-color: #F5F5F5;
	}

	.txt {
		overflow: hidden;
		width: 100%;
		text-overflow: ellipsis;
		font-size: 26rpx;
		white-space: nowrap;
	}

	.red {
		color: red;
		font-style: 28rpx;
	}

	.red text {
		text-decoration: line-through;
		color: #666666;
		font-size: 24rpx;
	}

	.php {
		width: 100%;
		height: auto;
	}

	.php-nav {
		width: 100%;
		height: 1112upx;
	}

	.php image {
		width: 100%;
		height: 100%;
	}

	.php>>>img {
		width: 100%;
	}

	.dd {
		width: 100%;
		height: 80rpx;
		text-align: center;
		line-height: 80rpx;
	}

	.dd-nav {
		color: #666;
		font-size: 28rpx;
	}

	.bg {
		width: 100%;
		height: 100%;
		background: rgba(0, 0, 0, 0.5);
		z-index: 10;
		position: fixed;
		left: 0;
		top: 0;
	}

	.ag {
		width: 100%;
		height: 100%;
		background: rgba(0, 0, 0, 0.5);
		z-index: 10;
		position: fixed;
		left: 0;
		top: 0;
	}

	.cg {
		width: 100%;
		height: 100%;
		background: rgba(0, 0, 0, 0.5);
		z-index: 10;
		position: fixed;
		left: 0;
		top: 0;
	}

	.bar {
		width: 100%;
		height: 479.39px;
		z-index: 100;
		background-color: #FFFFFF;
		position: fixed;
		right: 0;
		bottom: -980upx;
		transition-duration: 0.8s;
		border-top-left-radius: 20rpx;
		border-top-right-radius: 20rpx;
	}

	.bar-top {
		width: 710rpx;
		height: 70rpx;
		line-height: 70rpx;
		text-align: center;
		font-weight: bold;
		border-bottom: 1px solid #CCCCCC;
		margin: 20rpx;
	}

	.bar-nav {
		width: 710rpx;
		height: 400rpx;
		margin: 20rpx;
		padding-bottom: 20rpx;
	}

	.bar-nav>view {
		width: 100%;
		height: 60rpx;
		line-height: 60rpx;
		font-size: 28rpx;
		margin-bottom: 10rpx;
	}

	.bar-nav image {
		color: #FD6801;
	}

	#bar-der {
		width: 100%;
		height: 100rpx;
		line-height: 100rpx;
		text-align: center;
		color: white;
		font-size: 30rpx;
		background-color: #FD6801;
		position: absolute;
		bottom: 0;
		left: 0;
	}

	.gray {
		padding-left: 40rpx;
		color: gray;
		font-size: 28rpx;
	}

	.top-nav {
		width: 100%;
		height: 70%;
		/* background-color: burlywood; */
	}

	.swiper {
		width: 100%;
		height: 100%;
	}

	.in-be {
		width: 100%;
		height: 120rpx;
		line-height: 120rpx;
		/* background-color: #4CD964; */
		border-bottom: 1rpx solid #ccc;
		padding-bottom: 20rpx;
		/* margin-bottom: 20rpx; */
	}

	.in-below {
		width: 100%;
		height: 100rpx;
		line-height: 100rpx;
		text-align: center;
		color: white;
		font-size: 30rpx;
		background-color: #FD6801;
		position: absolute;
		bottom: 0;
		left: 0;
	}

	.be-shop {
		width: 100%;
		height: 100rpx;
		line-height: 100rpx;
		text-align: center;
		color: white;
		font-size: 30rpx;
		background-color: #FD6801;
		position: absolute;
		bottom: 0;
		left: 0;
	}

	.be-top {
		width: 100%;
		height: 250upx;
		/* background-color: #4CD964; */
	}

	.be-nav {
		width: 95%;
		height: 500upx;
		/* background-color: #007AFE; */
		margin: auto;
		border-bottom: 1upx solid #ccc;
		padding-bottom: 10rpx;
	}

	.be-left {
		float: left;
		display: flex;
		width: 35%;
		height: 100%;
	}

	.be-right {
		width: 65%;
		height: 100%;
		float: left;
		display: flex;
		align-items: center;
		/* line-height: 125rpx; */
	}

	.be-in-right {
		width: 100%;
		height: 50%;
	}

	.be-list {
		width: 100%;
		height: 100upx;
		/* background-color: #4CD964; */
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
		margin-top: 10upx;
	}

	.be-ing {
		float: left;
		width: 200upx;
		height: 80upx;
		line-height: 80upx;
		text-align: center;
		/* margin-left: 20upx; */
		background-color: #F8F9FB;
	}

	.btn {
		width: 95%;
		margin: auto;
		height: 90upx;
		line-height: 90upx;
		display: flex;
		align-items: center;
		justify-content: space-between;
		/* background-color: #4CD964; */
	}

	.buy {
		width: 80%;
		height: 100%;
	}

	.opx {
		width: 20%;
		height: 100%;
		display: flex;
		text-align: center;
		justify-content: space-around;
	}

	.opx-a {
		width: 33%;
		height: 100%;
	}

	.opx-b {
		width: 33%;
		height: 100%;
	}

	.opx-c {
		width: 33%;
		height: 100%;
	}
</style>
