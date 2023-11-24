<template>
	<view>
		<swiper class="swiper"  :autoplay="true" :interval="3000" :duration="1000">
			<swiper-item class="item" v-for="(item,index) in swiper" :key="index"> 
			<view class="title">{{item.title}}</view>
				<image class="img" :src="'http://124.93.196.45:10001'+item.imgUrl" mode="aspectFill"></image>
			</swiper-item>
		</swiper>	
		
		<view class="list">
			<view class="list-item" v-for="(item,index) in list" :key="index">
				<view class="box">
					
					<view class="title">{{item.title}}</view>
					<view class="detail">{{item.detail}}</view>
					
					<view class="requireText">要求：{{item.requireText}}</view>
					<view class="box2">
						
						<view class="undertaker">{{item.undertaker}}</view>
						<view class="startAt">{{item.startAt}}</view>
					</view>
					
				</view>
			</view>
		</view> 
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				token:uni.getStorageSync('token'),
				swiper:'',
				list:''
			}
		},
		onLoad() {
			this.getswiper(),
			this.getlist(),
			console.log(this.swiper);
		},
		methods: {
			getswiper(){
				uni.request({
					url:"http://124.93.196.45:10001/prod-api/api/volunteer-service/ad-banner/list",
					header:{
						Authorization:this.token
					},
					success: (res) => {
						this.swiper = res.data.data
						console.log(res);
					}
				})
			},
			getlist(){
				uni.request({
					url:"http://124.93.196.45:10001/prod-api/api/volunteer-service/activity/list",
					header:{
						Authorization:this.token,
					},
					success: (res) => {
						this.list=res.data.rows
						console.log(res);
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
			}
		}
	}
</script>

<style lang="scss">
	.swiper{
		width: 95%;
		height: 440rpx;
		// background-color: red;
		border-radius: 30rpx;
		margin: 0 auto;
		margin-top: 20rpx;
		.item{
			width: 100%;
			height: 400rpx;
			border-radius: 30rpx;
		}
		.img{
			width: 100%;
			height: 400rpx;
			border-radius: 30rpx;
		}
		.title{
			text-align: center;
			margin-left: 30rpx;
			font-size: 10rpx;
			position: relative;
			
			
			overflow: hidden;
			max-width: 600rpx;
			display: -webkit-box;
			-webkit-box-orient: vertical;
			-webkit-line-clamp: 1;
		}
	}
	.list{
		width: 95%;
		margin: 0 auto;
		margin-top: 10rpx;
	}
	.list-item{
		border-radius: 30rpx;
		border: 4rpx solid #f1f1f1;
		width: 100%;
		background-color: #f1f1f1;
		margin-top: 20rpx;
	}
	.box2{
		font-size: 30rpx;
		margin-top: 20rpx;
		display: flex;
		justify-content: space-between;
		// background-color: purple;
		
	}
	.title{
		font-size: 40rpx;
		font-weight: 700;
		text-align: center;
	}
	.detail{
		margin-top: 10rpx;
		text-align: left;
	}
	.requireText{
		text-align: center;
		margin-top: 10rpx;
		font-size: 35rpx;
		font-weight: 700;
	}
</style>
