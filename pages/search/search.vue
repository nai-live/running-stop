<template>
	<view :class="{body:show==towshow}">
		<!-- 搜索栏 -->
		<view class="top-seek">
			<view class="top-left">
				<view class="top-leftpicbox" @click="back">
					<image class="top-leftpic" src="../../static/search-pic2.png"></image>
				</view>
			</view>
			<view class="top-centre">
				<view class="seek">
					<view class="seek-box">
						<image class="seek-pic" src="../../static/index-pic2.png"></image>
					</view>
					<view class="seek-inputbox">
						<input class="seek-input" type="text" placeholder="输入搜索关键词" v-model="changeVaule">
					</view>
				</view>
			</view>
			<view class="top-right" @click="searchs">
				搜索
			</view>
		</view>
		<!-- 热门搜索 第一个页面-->
		<view class="one-text" v-show="oneshow">
			<view class="host">
				<view class="host-text">热门搜索</view>
				<view class="host-picbox">
					<image class="host-pic" src="https:\/\/tangzhe123-com.oss-cn-shenzhen.aliyuncs.com\/public\/5d8833ed94392.png"></image>
				</view>
				<view class="book-box">
					<text>领卷中心</text>
					<text>Redmi K20</text>
					<text>RedmiBook 14</text>
					<text>智能积木 越野四驱车</text>
					<text>手环 腕带</text>
				</view>
			</view>
			<!-- 常用分类 -->
			<view>
				<view class="host-texts">常用分类</view>
				<view class="link-text">
					<text>耳机</text>
					<text>手机</text>
					<text>音箱</text>
					<text>手表</text>
					<text>配件</text>
					<text>健康</text>
					<text>酷玩</text>
				</view>
			</view>
			<!-- 搜索记录 -->
			<view class="seek-sear">
				<view class="seek-cord">搜索记录</view>
				<text @click="ttext">{{shopnames}}</text>
				<text>小米8屏幕指纹版</text>
			</view>
		</view>
		
		<!-- 综合栏 第二个页面-->
		<view class="tow-text" v-show="towshow">
			<!-- <view class="content">
				 导航 
				<view class="size">
					<view class="size-box">
						<view class="size-text">
							<text>综合</text>
						</view>
						<view class="size-picbox">
							<image class="size-pic" src="../../static/search-pic1.png"></image>
						</view>
					</view>
					<view class="size-box">
						<view class="size-text">
							<text>销量</text>
						</view>
						<view class="size-picbox">
							<image class="size-pic" src="../../static/search-pic1.png"></image>
						</view>
					</view>
					<view class="size-box">
						<view class="size-text">
							<text>价格</text>
						</view>
						<view class="size-picbox">
							<image class="size-pic" src="../../static/search-pic1.png"></image>
						</view>
					</view>
					<view class="size-box">
						<view class="size-text" @click="hide">
							<text>筛选</text>
						</view>
					</view>
				</view>
			</view>
			
			 内容 
			<view>
				<view class="shop-boxs" v-for="(item,index) in seekresult" :key= "item.id">
					<view class="shop-leftbox">
						<view class="shop-picbox">
							<image class="shop-img" :src="item.cover"></image>
						</view>
					</view>
					<view class="shop-rightbox">
						<view class="shop-name">{{item.title}}</view>
						<view class="shop-syn">{{item.desc}}</view>
						<view class="shop-num">{{item.min_price}}</view>
					</view>
				</view>
			</view> -->
			 <!-- 弹出页 -->
			<view class="box" v-show="show">
			<view class="black-box" @click="blacks"></view>
				<view class="white-box">
					<view class="fuwu">服务</view>
					<view class="serves">
						<text class="borbox" :data-id="index" @click="getBat" :class="{borboxs:active==index}" v-for="(item,index) in serve"
						 :key="item.id">{{item}}</text>
					</view>
					<view class="fenlei">分类</view>
					<view class="rserves">
						<text class="borbox" :data-id="index" @click="getBats" :class="{borboxs:actives==index}" v-for="(item,index) in rserve"
						 :key="item.id">{{item}}</text>
					</view>
					<view class="bottom-box">
						<text class="bottom-left" @click="reset">重置</text>
						<text class="bottom-right" @click="shows">确认</text>
					</view>
				</view>
			</view>
			<List  @getHide='getHide' :title="changeVaule"></List>
		</view>
	</view>
</template>

<script>
	import List from '../List/list'
	export default {
		components:{
		  List
		},
		data(){
			return{
				serve: ['促销', '分期', '仅看有货'], //弹出页数据
				rserve: ['耳机', '户外', '配件'],	//弹出页数据
				active: 0,		 //弹出页下标
				actives: 0,		 //弹出页下标
				show: false,	 //弹出页显示
				oneshow: true,	 //搜索记录页面
				towshow: false,	 //搜索结果页面
				changeVaule: '', // 输入框输入的值
				seekresult : []	 ,//搜索结果
				shopnames:'小米'	//搜索记录
			}
		},
		methods: {
			getBat(e) {				//弹出页文字选择点击事件1
				let index = e.currentTarget.dataset.id
				this.active = index
			},
			getBats(e) {			//弹出页文字选择点击事件2
				let indexs = e.currentTarget.dataset.id
				this.actives = indexs
			},
			getHide() {				//弹出页显示
				this.show = true
			},
			shows() {				//弹出页隐藏
				this.show = false
			},
			reset() {				//弹出重置
				this.active = 0
				this.actives = 0
			},
			searchs(){				//搜索
				this.oneshow = false
				this.towshow = true
				// uni.request({
				// 	url: 'http://ceshi3.dishait.cn/api/goods/search',
				// 	data: {
				// 		title : this.changeVaule,
				// 		page : 1
				// 	},
				// 	method:'POST',
				// 	success: (res) => {
				// 		this.seekresult=res.data.data
				// 	}
				// })
				
			},
			back() {			//返回
				uni.navigateBack({
					delta: 1
				})	
			},
			blacks(){			//遮罩层
				this.show = false
			},
			ttext(){			//搜索记录
				this.changeVaule = this.shopnames
				this.oneshow = false
				this.towshow = true
				uni.request({
					url: 'http://ceshi3.dishait.cn/api/goods/search',
					data: {
						title : this.changeVaule,
						page : 1
					},
					method:'POST',
					success: (res) => {
						this.seekresult=res.data.data
					}
				})
			}
			
		}
		
	}
</script>

<style>
	.body{
		overflow: hidden;
		position: fixed; 
	}
	/* 热门 */
	.host {
		width: 100%;
		height: 480upx;
		margin-bottom: 40upx;
	}

	.host-text {
		width: 100%;
		height: 100upx;
		line-height: 100upx;
		text-indent: 40upx;
		font-size: 34upx;
	}

	.host-texts {
		width: 100%;
		height: 100upx;
		line-height: 100upx;
		text-indent: 40upx;
		font-size: 34upx;
		margin-top: 150upx;
	}

	.host-picbox {
		width: 100%;
		height: 200upx;
	}

	.host-pic {
		width: 100%;
		height: 100%;
	}

	.book-box {
		width: 90%;
		height: 350upx;
		margin-left: 10upx;
	}

	.book-box text {
		border: 1px solid #E7A8AC;
		width: auto;
		height: 44upx;
		padding: 10upx;
		display: inline-block;
		font-size: 32upx;
		margin: 20upx;
		background-color: #F8EAE9;
	}

	.link-text {
		width: 80%;
		height: 200upx;
	}

	.link-text text {
		font-size: 30upx;
		display: inline-block;
		width: auto;
		height: 42upx;
		background-color: #F5F5F5;
		padding: 15upx;
		margin: 20upx;
	}

	/* 搜索记录 */
	.seek-cord {
		width: 100%;
		height: 100upx;
		border-top: 8px solid #F5F5F5;
		border-bottom: 1px solid #ccc;
		line-height: 100upx;
		text-indent: 20upx;
		font-weight: 600;
	}

	.seek-sear text {
		width: 100%;
		height: 100upx;
		border-bottom: 1px solid #ccc;
		line-height: 100upx;
		text-indent: 25upx;
		display: block;
	}
	.shopcontents{
		width: 100%;
		height: 1000upx;
		overflow: hidden;
	}
	.shopcontent{
		width: 100%;
		height: 100%;
	}
	.content{
		margin-top: 10upx;
	}
	.size {
		width: 100%;
		height: 100upx;
		border-top: 1px solid #ccc;
		border-bottom: 1px solid #ccc;
	}
	
	.size-box {
		float: left;
		width: 25%;
	}
	
	.size-picbox {
		float: left;
		width: 40upx;
		height: 40upx;
		line-height: 115upx;
	}
	
	.size-pic {
		width: 100%;
		height: 100%;
		line-height: 100upx;
	}
	
	.size-text {
		float: left;
		line-height: 100upx;
		margin-left: 45upx;
	}
	
	.box {
		width: 100%;
		height: 100%;
		z-index: 999;
		position: fixed; 
		bottom: 0px;
		left: 0px;
	}
	
	.black-box {
		width: 100%;
		height: 100%;
		background-color: #333333;
		opacity: 0.5;
		z-index: 9;
		position: fixed;
		bottom: 0px;
		left: 0px;
	}
	
	.white-box {
		width: 80%;
		height: 100%;
		background-color: white;
		z-index: 99;
		position: absolute;
		bottom: 0px;
		right: 0px;
	}
	
	.fuwu,
	.fenlei {
		width: 100%;
		height: 100upx;
		line-height: 100upx;
		text-indent: 20upx;
	}
	
	.serves,
	.rserves {
		width: 100%;
		height: 80upx;
		display: flex;
		justify-content: space-around;
		margin-top: 10upx;
		margin-bottom: 80upx;
	}
	
	.borbox {
		width: auto;
		height: 70upx;
		padding: 0upx 40upx;
		line-height: 70upx;
		background-color: #F8F9FB;
		border-radius: 5px;
	}
	
	.borboxs {
		width: auto;
		height: 70upx;
		padding: 0upx 40upx;
		line-height: 70upx;
		background-color: #FCE0D5;
		border-radius: 5px;
		color: #EE7927;
	}
	
	.bottom-box {
		width: 100%;
		height: 100upx;
		position: absolute;
		bottom: 0px;
	}
	
	.bottom-left {
		display: inline-block;
		width: 50%;
		height: 100upx;
		text-align: center;
		line-height: 100upx;
	}
	
	.bottom-right {
		display: inline-block;
		width: 50%;
		height: 100upx;
		text-align: center;
		line-height: 100upx;
		background-color: #FD6801;
		color: white;
	}
	
	
	.top-seek {
		width: 100%;
		height: 80upx;
	}
	
	.top-left {
		width: 12%;
		height: 80upx;
		float: left;
	}
	
	.top-centre {
		width: 72%;
		height: 80upx;
		float: left;
	}
	
	.top-right {
		width: 14%;
		height: 80upx;
		float: left;
		text-align: center;
		line-height: 80upx;
		font-weight: 700;
		font-size: 34upx;
	}
	
	.top-leftpicbox {
		width: 55upx;
		height: 55upx;
		margin-left: 35%;
		margin-top: 15upx;
	}
	
	.top-leftpic {
		width: 100%;
		height: 100%;
		text-align: center;
	}
	
	.seek {
		width: 100%;
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
		width: 470upx;
		margin-top: 8upx;
		font-size: 24upx;
	}
	
	.seek-input {
		width: 100%;
		height: 70upx;
		background: #F7F7F7;
		border-radius: 10upx;
	
	}
	
	/* 内容 */
	.shop-boxs{
		width: 100%;
		height: 300upx;
		border: 1px solid #ccc;
	}
	.shop-leftbox{
		width: 40%;
		height: 100%;
		float: left;
	}
	.shop-rightbox{
		width: 59%;
		height: 100%;
		float: right;
	}
	.shop-picbox{
		width: 90%;
		height: 90%;
		margin: auto;
		margin-top: 15upx;
	}
	.shop-img{
		width: 100%;
		height: 100%;
	}
	.shop-name{
		font-size: 40upx;
		font-weight: 900;
		margin-bottom: 10upx;
		margin-top: 30upx;
	}
	.shop-syn{
		font-size: 26upx;
		color: #999;
		margin-bottom: 10upx;
	}
	.shop-num{
		font-size: 40upx;
		color: #EE7927;
		font-weight: 600;
		margin-bottom: 10upx;
		margin-left: 15upx;
	}
</style>
