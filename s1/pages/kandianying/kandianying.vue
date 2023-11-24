<template>
	<view>
		<swiper class="swiper" :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
			<swiper-item class="item" v-for="(item,index) in swiper" :key="index">
				<image  class="item-img" :src="'http://124.93.196.45:10001'+item.advImg" mode="aspectFill"></image>
			</swiper-item>
		</swiper>
		<view class="nav">
			<view class="nav-item"></view>
		</view>
		
		
	</view>
</template>

<script>
		export default {
			data() {
				return {
					swiper:[]
				}
			},
		onLoad() {
			this.getswiper()
		},
		methods: {
			getswiper(){
				uni.request({
					url:"http://124.93.196.45:10001/prod-api/api/movie/rotation/list",
					success: (res) => {
						this.swiper = res.data.rows
						// console.log(res);
					}
				})
			}
		}
	}
</script>

<style lang="scss">
	.swiper{
		width: 95%;
		height: 480rpx;
		// background-color: red;
		margin: 0 auto;
		margin-top: 10rpx;
		border-radius: 30rpx;
		.item-img{
			width: 100%;
			height: 480rpx;
			border-radius: 30rpx;
		}
	}
</style>
