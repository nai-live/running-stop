<template>
	<view>
		<!-- 导航栏 -->
		<view class="nav">
			<view class="news">
				<image class="news-pic" src="../../static/timg.jpg"></image>
			</view>
			<view class="seek" @click="goIn('Search/search')">
				<view class="seek-box">
					<image class="seek-pic" src="../../static/10.jpg"></image>
				</view>
				<view class="seek-inputbox">
					<view class="seek-input">
						输入搜索关键词
					</view>
					
					<!-- <input class="seek-input" type="text" placeholder="输入搜索关键词"> -->
				</view>
			</view>
			<view class="code">
				<image class="code-pic" src="../../static/index-pic3.png"></image>
			</view>
		</view>

		<!-- 菜单栏 -->
		<view class="bar">
			<scroll-view class="swiper-tab" scroll-x>
				<block v-for="(item,index) in tabBars" :key="item.id">
					<view :data-id="index" class="con-text" @tap="setCurr">
						<text class="swiper-text" :class="{nnone:curr==index}">
							{{item.name}}
						</text>
						
					</view>
				</block>
			</scroll-view>
		</view>
		<!-- 内容 -->
		<swiper class="content-box" :current="curr" @change="setCurr" :style="hig">
			<swiper-item>
				<scroll-view scroll-y="true" style="height: 100%;" >
					<!-- 轮播1 -->
					<view class="uni-padding-wrap">
						<view class="page-section swiper">
							<view class="page-section-spacing">
								<swiper class="big-box" :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval" :duration="duration">
									<swiper-item v-for="(item,index) in picbox" class="swiper-pic" :key="item.id">
										<image :src="item.src" class="pic-box"></image>
									</swiper-item>
								</swiper>
							</view>
						</view>
					</view>
					<!-- 商品选择栏 -->
					<view class="shopping-box">
						<view class="in-box">
							<view class="all-box" v-for="(item,index) in shopping" :key="item.id"  @tap="goIno(item.text)">
								<view class="shoppic-box">
									<image class="shop-pic" :src="item.src"></image>
								</view>
								<text class="shop-text">{{item.text}}</text>
							</view>
						</view>
					</view>
					<!-- 三张宣传图 -->
					<view class="three-pic">
						<view class="left-box">
							<image class="left-pic" :src="onepic[0].src"></image>
						</view>
						<view class="right-box">
							<view class="right-boxpic1">
								<image class="pic1" :src="onepic[1].src"></image>
							</view>
							<view class="right-boxpic2">
								<image class="pic2" :src="onepic[2].src"></image>
							</view>
						</view>
					</view>
					<!-- 每日精选 -->
					<view class="everyday">
						<text class="day-text">{{day.title}}</text>
						<view class="daypic-box">
							<image class="day-pic" src="https://tangzhe123-com.oss-cn-shenzhen.aliyuncs.com/public/5d8833ed94392.png"></image>
						</view>
					</view>
					<!-- 商品详情 -->
					<view class="shop-bigbox">
						<view class="one-bigbox" v-for="(item,index) in detail" :key="item.id">
							<view class="detail-picbox">
								<image class="detail-pic" :src="item.cover"></image>
							</view>
							<view class="shop-name">{{item.title}}</view>
							<view class="shop-detail">{{item.desc}}</view>
							<view class="shop-tow">
								<text class="shop-newnum">¥{{item.oprice}}</text>
								<text class="shop-oldnum">¥{{item.pprice}}</text>
							</view>
						</view>
					</view>
				</scroll-view>
			</swiper-item>
			<swiper-item>
				<scroll-view  scroll-y="true" style="height: 100%;">
					<!-- 轮播1 -->
					<view class="uni-padding-wrap">
						<view class="page-section swiper">
							<view class="page-section-spacing">
								<swiper class="big-box" :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval" :duration="duration">
									<swiper-item v-for="(item,index) in picbox" class="swiper-pic" :key="item.id">
										<image :src="item.src" class="pic-box"></image>
									</swiper-item>
								</swiper>
							</view>
						</view>
					</view>
					<!-- 商品选择栏 -->
					<view class="shopping-box">
						<view class="in-box">
							<view class="all-box" v-for="(item,index) in shopping" :key="item.id" @tap="goIno(item.text)">
								<view class="shoppic-box">
									<image class="shop-pic" :src="item.src"></image>
								</view>
								<text class="shop-text">{{item.text}}</text>
							</view>
						</view>
					</view>
					<!-- 三张宣传图 -->
					<view class="three-pic">
						<view class="left-box">
							<image class="left-pic" :src="onepic[0].src"></image>
						</view>
						<view class="right-box">
							<view class="right-boxpic1">
								<image class="pic1" :src="onepic[1].src"></image>
							</view>
							<view class="right-boxpic2">
								<image class="pic2" :src="onepic[2].src"></image>
							</view>
						</view>
					</view>
					<!-- 每日精选 -->
					<view class="everyday">
						<text class="day-text">{{day.title}}</text>
						<view class="daypic-box">
							<image class="day-pic" src="https://tangzhe123-com.oss-cn-shenzhen.aliyuncs.com/public/5d8833ed94392.png"></image>
						</view>
					</view>
					<!-- 商品详情 -->
					<view class="shop-bigbox">
						<view class="one-bigbox" v-for="(item,index) in detail" :key="item.id">
							<view class="detail-picbox">
								<image class="detail-pic" :src="item.cover"></image>
							</view>
							<view class="shop-name">{{item.title}}</view>
							<view class="shop-detail">{{item.desc}}</view>
							<view class="shop-tow">
								<text class="shop-newnum">¥{{item.oprice}}</text>
								<text class="shop-oldnum">¥{{item.pprice}}</text>
							</view>
						</view>
					</view>
				</scroll-view>
			</swiper-item>
			<swiper-item>
				<scroll-view>
					智能
				</scroll-view>
			</swiper-item>
			<swiper-item>
				<scroll-view>
					电视
				</scroll-view>
			</swiper-item>
			<swiper-item>
				<scroll-view>
					笔记本
				</scroll-view>
			</swiper-item>
			<swiper-item>
				<scroll-view>
					家电
				</scroll-view>
			</swiper-item>
			<swiper-item>
				<scroll-view>
					生活周边
				</scroll-view>
			</swiper-item>
		</swiper>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				indicatorDots: true, //是否显示面板指示点
				autoplay: true, //是否自动切换
				interval: 2000, //自动切换时间间隔
				duration: 500, //滑动动画时长
				tabBars: [], //菜单栏	
				index: '', //每个菜单栏的id
				curr: 0, //菜单栏所对应内容的下标
				picbox: [], //轮播图1
				shopping: [], //商品选择栏
				onepic: [], //三张宣传图
				day: [], //每天精选
				detail: [], //商品详情
				scrollTop: 0,
				hig:''
			}
		},
		onLoad() {
			let _that = this
			   uni.getSystemInfo({
			       success: function (res) {
			           _that.hig = "height: "+(res.windowHeight-90)+"px";
			     console.log(_that.hig)
			       }
			   });
			uni.request({
				url: 'http://ceshi3.dishait.cn/api/index_category/data',
				success: (res) => {
					this.tabBars = res.data.data.category //初始的时候获取菜单栏文字
					this.index = res.data.data.category.id //初始的时候获取菜单栏文字的id
					console.log(this.tabBars)
				}
			})
			uni.request({
				url: 'http://ceshi3.dishait.cn/api/index_category/1/data/1',
				success: (res) => {
					console.log(res.data.data[1].data)
					this.picbox = res.data.data[0].data //轮播1
					this.shopping = res.data.data[1].data //商品选择栏
					this.onepic = res.data.data[2].data //三张宣传图
					this.day = res.data.data[3].data //每日精选
					this.detail = res.data.data[4].data //商品详情
				}
			})
		},
		methods: {
			setCurr(e) {
				let thisCurr = e.detail.current || e.currentTarget.dataset.id || 0;
				this.curr = thisCurr;
			},
			goIn(e){
				uni.navigateTo({
					url: "../" + e
				})
			},
			goIno(e){
				console.log(1111)
				if(e == "新品发布"){
					console.log(111)
					uni.navigateTo({
						url: "../Lists/lists"
					})
					return;
				}
			}
		}
	}
</script>

<style scoped>
	/* 导航栏 */
	.nav {
		width: 100%;
		height: 80upx;
	}

	.news {
		width: 10%;
		height: 80upx;
		float: left;
	}

	.news-pic {
		width: 60upx;
		height: 60upx;
		margin-top: 14upx;
		margin-left: 10upx;
	}

	.seek {
		width: 78%;
		height: 80upx;
		float: left;
		position: relative;
	}

	.seek-box {
		width: 70upx;
		height: 70upx;
		background: #F7F7F7;
		float: left;
		margin-top: 8upx;

	}

	.seek-pic {
		width: 30upx;
		height: 30upx;
		margin-left: 25upx;
		margin-top: 25upx;
	}

	.seek-inputbox {
		float: left;
		width: 510upx;
		margin-top: 8upx;
		font-size: 24upx;
	}

	.seek-input {
		width: 100%;
		height: 70upx;
		background: #F7F7F7;
		border-radius: 10upx;
		line-height: 70upx;
		text-align: center;
	}

	.code {
		width: 10%;
		height: 80upx;
		float: left;
	}

	.code-pic {
		width: 55upx;
		height: 55upx;
		margin-top: 14upx;
		margin-left: 10upx;
	}

	/* 菜单 */
	.bar {
		width: 100%;
		height: 62upx;
		margin-top: 30upx;
		margin-bottom: 4upx;
	}

	.swiper-tab {
		width: 90%;
		white-space: nowrap;
		margin: auto;
	}
	.swiper-text{
		width: auto;
		height: 62upx;
	}
	.con-text {
		display: inline-block;
		width: 20%;
		height: 80upx;
	}

	.nnone {
		display: inline-block;
		width: auto;
		height: 62upx;
		/* margin-left: 45upx; */
		color: #FD6801;
		border-bottom: 2px solid #FD6801;
	}

	.active {
		display: inline-block;
		width: auto;
		height: 60upx;
		margin-left: 45upx;
		border-top: 1px solid red;

	}

	/* 轮播1 */
	.content-box {
		width: 100%;
		height: 3200upx;
		background-color: #F7F7F7;
	}

	.big-box {
		width: 100%;
		height: 350upx;
	}

	.pic-box {
		width: 100%;
		height: 100%;
	}

	/* 商品选择栏 */
	.shopping-box {
		width: 100%;
		height: 350upx;
		background-color: #FFFFFF;
		margin-bottom: 20upx;
	}

	.in-box {
		width: 87%;
		height: 350upx;
		display: flex;
		justify-content: space-around;
		flex-wrap: wrap;
		margin: auto;
		padding-top: 40upx;
	}

	.all-box {
		width: 20%;
		text-align: center;
	}

	.shoppic-box {
		width: 65upx;
		height: 65upx;
		margin: auto;
	}

	.shop-pic {
		width: 100%;
		height: 100%;
	}

	.shop-text {
		font-size: 20upx;
	}

	/* 三张图片 */
	.three-pic {
		width: 100%;
		height: 500upx;
	}

	.left-box {
		width: 49.5%;
		height: 500upx;
		float: left;
	}

	.right-box {
		width: 50%;
		height: 500upx;
		float: left;
	}

	.left-pic {
		width: 100%;
		height: 100%;
	}

	.right-boxpic1,
	.right-boxpic2 {
		width: 100%;
		height: 50%;
	}

	.pic1,
	.pic2 {
		width: 100%;
		height: 100%;
	}

	/* 每日精选 */
	.everyday {}

	.day-text {
		width: 100%;
		height: 75upx;
		display: block;
		background: #FFFFFF;
		line-height: 75upx;
		text-indent: 30upx;
		font-weight: 700;
		font-size: 30upx;
	}

	.daypic-box {
		width: 100%;
		height: 380upx;
	}

	.day-pic {
		width: 100%;
		height: 100%;
	}

	/* 商品详情 */
	.one-bigbox {
		width: 49.3%;
		height: 510upx;
		float: left;
		margin-right: 5upx;
	}

	.detail-picbox {
		width: 100%;
		height: 350upx;
	}

	.detail-pic {
		width: 100%;
		height: 100%;
	}

	.shop-name {
		font-size: 28upx;
		text-indent: 15upx;
		margin-top: 10upx;
	}

	.shop-detail {
		font-size: 22upx;
		color: #999999;
		overflow: hidden;
		text-overflow: ellipsis;
		white-space: nowrap;
		text-indent: 15upx;
		margin-top: 5upx;
		margin-bottom: 8upx;
	}

	.shop-tow {
		text-indent: 15upx;
	}

	.shop-newnum {
		color: #FD6801;
	}

	.shop-oldnum {
		color: #999999;
		font-size: 20upx;
		margin-left: 20upx;
	}
</style>
