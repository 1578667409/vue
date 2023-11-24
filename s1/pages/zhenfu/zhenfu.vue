<template>
	<view>
		<swiper class="swiper" :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
			<swiper-item class="item" v-for="(item,index) in swiper" :key="index">
				<image class="img" :src="'http://124.93.196.45:10001/'+item.imgUrl" mode="aspectFill"></image>
			</swiper-item>
		</swiper>
		
		<view class="nav">
			<view class="nav-item" v-for="(item,index) in nav" :key="index">
				<image class="nav-img" :src="'http://124.93.196.45:10001/'+item.imgUrl" mode="aspectFit"></image>
				<view class="nav-title">{{item.name}}</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				token:uni.getStorageSync('token'),
				swiper:[],
				nav:[]
			}
		},
		onLoad() {
			
			this.getswiper()
			this.getnav()
		},
		methods: {
			getswiper(){
				uni.request({
					url:'http://124.93.196.45:10001/prod-api/api/gov-service-hotline/ad-banner/list',
					header:{
						Authorization:this.token
					},
					success: (res) => {
						this.swiper=res.data.data
						if(res.data.code==401){
							uni.showModal({
								title:'登录啊蠢卵',
								success:function(res){
									if(res.confirm){
										uni.navigateBack()
									}else{
										uni.navigateBack()
									}
								}
							})
						}
					}
				})
			},
			getnav(){
				uni.request({
					url:'http://124.93.196.45:10001/prod-api/api/gov-service-hotline/appeal-category/list',
					header:{
						Authorization:this.token
					},
					success: (res) => {
						this.nav=res.data.rows
					}
				})
			}
		}
	}
</script>

<style lang="scss">
	.swiper{
		height: 400rpx;
		margin: 2% 3%;
		.item{
			display: flex;
			justify-content: center;
			.img{
				height: 400rpx;
				width: 100%;
				border-radius: 15rpx;
			}
		}
	}
	
	.SviceNav{
		display: flex;
		flex-wrap: wrap;
		justify-content: space-evenly;
		.SviceNav-item{
			width: 130rpx;
			padding: 15rpx;
			.SviceNav-img{
				height: 130rpx;
				width: 130rpx;
			}
			.SviceNav-text{
				text-align: center;
			}
		}
	}
	.nav-item{	
		// margin-left: 2rpx;
		padding: 15rpx;
		margin-top: 60rpx;
		float: left;
		justify-content: space-around;
		flex-wrap: wrap;
		justify-content: center;
	}
	.nav-img{
		
		width: 150rpx;
		height: 150rpx;
	}
	.nav-title{
		position: absolute;
		text-align: center;
		// margin-left: 30rpx;
		font-size: 12rpx;
		margin-left: 25rpx;
	}
</style>
