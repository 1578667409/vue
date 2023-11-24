<template>
	<view class="content">
		<input type="text" class="input" placeholder="请输入">
		<swiper class="swiper" :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
			<swiper-item class="swiper-item" v-for="(item,index) in swiper" :key="index">
				<image class="swiper-img" :src="'http://124.93.196.45:10001'+item.advImg" mode="aspectFill"></image>
			</swiper-item>
		</swiper>
		
		
		<view class="all">
			<view class="top">推荐服务</view>
			
			<view class="all-item" @click="cliall(item.id)"   v-for="(item,index) in all.slice(0,9)" :key="index">
				<image class="all-img" :src="'http://124.93.196.45:10001'+item.imgUrl"  mode=""></image>
				<view class="all-text">{{item.serviceName}}</view>
			</view>
			
			<view class="all-more">	
				<image class="more-img" src="../../static/logo.png" mode=""></image>
				<view class="all-text">更多服务</view>
			</view>
		</view>
		
		<scroll-view scroll-x="ture" class="navscroll">
			<view class="item" v-for="item in 10">{{item.name}}</view>
			
		</scroll-view>
		
		
		<view class="news" >
			<view class="news-item" @click="clilist(item)"  v-for="(item,index) in news" :key="index">
				<image class="news-img" :src="'http://124.93.196.45:10001'+item.cover" mode="aspectFill"></image>
				<view class="news-text">
					<view class="news-title">{{item.title}}</view>
					<view class="news-time">发布时间：{{item.createTime}}</view>
				</view>
			</view>
		</view>
	
	
	</view>
</template>

<script>
	export default {
		data() {
			return {
				swiper:[],
				all:[],
				news:[]
				
			}
		},
		onLoad() {
			this.getSwiper(),
			this.getAll(),
			this.getNews(),
			this.clinav()
		},
		methods: {
			getSwiper(){
				uni.request({
					url:'http://124.93.196.45:10001/prod-api/api/rotation/list',
					success: (res) => {
						this.swiper = res.data.rows
					}
				})
			},
			getAll(){
				uni.request({
					url:"http://124.93.196.45:10001/prod-api/api/service/list",
					success: (res) => {
						this.all = res.data.rows
						console.log(this.all);
					}
				})
			},
			getnavscroll(){
				uni.request({
					url:"http://124.93.196.45:10001/prod-api/press/category/list",
					success: (res) => {
						this.navscroll=res.data.data
					}
				})
			},
			clilist(item){
				uni.navigateTo({
					url:`/pages/list/list?id=${item.id}`
				})
			},
			cliall(id){
				switch(id){
					case 29:
					uni.navigateTo({
						url:"/pages/zhenfu/zhenfu"
					})
					break;
					case 28:
					uni.navigateTo({
						url:'/pages/jiaoyu/jiaoyu'
					})
					break;
					case 30:
					uni.navigateTo({
						url:"/pages/shuzitushuguan/shuzitushuguan"
					})
					break;
					case 31:
					uni.navigateTo({
						url:"/pages/lj/lj"
					})
					break;
					case 32:
					uni.navigateTo({
						url:'/pages/zhiyuan/zhiyuan'
					})
				}
			},
			clinav(){
				
			},
			getNews(){
				uni.request({
					url:"http://124.93.196.45:10001/prod-api/press/press/list",
					success: (res) => {
						this.news = res.data.rows
					}
				})
			}
		}
	}
</script>

<style lang="scss">
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}
	.input{
		width: 95%;
		height: 60rpx;
		border: 1rpx solid #999;
		border-radius: 30rpx;
		margin-top: 20rpx;
		text-align: center;
	}
	.swiper{
		width: 95%;
		height: 350rpx;
		// background-color: red;
		margin-top: 15rpx;
		border-radius: 20rpx;
		.swiper-item{
			justify-content: center;
			display:flex;
		}
		.swiper-img{
			width: 100%;
			height: 350rpx;
			border-radius: 20rpx;
		}
	}
	.all{
		width: 95%;
		height: 370rpx;
		background-color:#f8f8f8;
		margin-top: 15rpx;
		border-radius: 30rpx;
		position: relative;
		.top{
			position: absolute;
			left:30rpx;
			top: 40rpx;
			// justify-content: center;
			// background-color: purple;
			height: 50rpx;
			// margin-top: 10rpx;
			border-bottom: 2rpx solid #fff;
		}
	}
	.all{
		display: flex;
		flex-wrap: wrap;
		justify-content: space-evenly;
		// background-color: blue;
	}
	.all-item{
		padding-top: 20rpx;
		// background-color: red;
		text-align:center;
		margin-top: 90rpx;
		width: 130rpx;
		height: 10rpx;
	}
	.all-more{
		padding-top: 20rpx;
		// background-color: red;
		text-align:center;
		margin-top: 90rpx;
		width: 130rpx;
		height: 120rpx;
	}
	.all-img,.more-img{
		border-radius: 50rpx;
		height: 80rpx;
		width: 80rpx;
	}
	.all-text{
		padding-left: 10rpx;
		padding-right: 10rpx;
		font-size: 20rpx;
		// font-size: 17rpx;
		// margin-left: -10rpx;
		text-align: center;
		colof: #999;
		
		max-width: 300rpx;  /*多长才会隐藏文字变成省略号*/
		overflow: hidden;
		display: -webkit-box; /** 对象作为伸缩盒子模型显示 **/
		-webkit-box-orient: vertical; /** 设置或检索伸缩盒对象的子元素的排列方式 **/
		-webkit-line-clamp: 1; /** 显示的行数 **/
		
		// 记住这五件套就行了
	}
	.news{
		width: 95%;
		
		
		// background-color: red;
		margin-top: rpx;
		border-radius: 30rpx;
		.news-item{
			display: flex;
			// border-bottom: 3rpx solid skyblue;
			border-top: 3rpx solid #999;
			position: relative;
			width: 100%;
			height: 200rpx;
			// background-color: purple;
			margin-bottom: 20rpx;
			
			// border-radius: 30rpx;
		}
		.news-text{
			
			display: flex;
			flex-direction: column;
			justify-content: space-between;
			padding-left: 20rpx;
			flex: 1;
			// margin-top: 20rpx;
			padding-top: 30rpx;
		}
		.news-img{
			float: left;
			top:20rpx;
			left: 10rpx;
			float: left;
			width: 250rpx;
			height: 180rpx;
			// border-radius: 30rpx;
			padding: 5rpx;
			
		}
		.news-title{
			overflow: hidden;
			display: -webkit-box;
			-webkit-box-orient: vertical;
			-webkit-line-clamp: 2;
			
		}
		.news-time{
			font-size: 10rpx;
		}
	}
	.navscroll{
		// border: 2rpx solid skyblue;
		background-color: #f7f8fa;
		margin-top: 20rpx;
		width: 95%;
		height: 60rpx;
		// background-color: red;
		
		// 不换行,必须加
		white-space: nowrap;
		
	}
	.item{
		padding: 0 30rpx;
		display: inline-block;
		
		line-height: 60rpx;
		text-align: center;
		// background-color: blue;
	}
	
</style>
