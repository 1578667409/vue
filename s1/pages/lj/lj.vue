<template>
	<view>
		<view class="box">
			<view class="item" v-for="(item,index) in box" :key="index">
				<image class="item-img" :src="'http://124.93.196.45:10001'+item.imgUrl" mode="aspectFit"></image>
				<view class="wenzi">
					<view class="title">{{item.name}}</view>
					<view class="introduce">定义:{{item.introduce}}</view>
					<view class="guide">{{item.guide}}</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				box:[],
				token:uni.getStorageSync('token')
			}
		},
		onLoad() {
			this.getbox()
		},
		methods: {
			getbox(){
				uni.request({
					url:'http://124.93.196.45:10001/prod-api/api/garbage-classification/garbage-classification/list',
					header:{
						Authorization:this.token,
					},
					success: (res) => {
						this.box = res.data.rows
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
	.item{
		justify-content: space-between;
		position: relative;
		// display: flex;
		width: 95%;
		height: 300rpx;
		// background-color: red;
		margin: 0 auto;
		margin-top: 30rpx;
		border: 4rpx solid skyblue;
		border-radius: 30rpx;
		.item-img{
			
			
			position:absolute;
			top: 60rpx;
			margin-top: -100rpx;
			width:200rpx;
			height:300rpx;
			padding: 40rpx;
			border-radius: 30rpx;
		}
		.title{
			
			position: absolute;
			// top: -50rpx;
			bottom: 225rpx;
			right: 30rpx;
			font-size:45rpx;
			font-weight: 700;
			margin-right: 150rpx;
			float: right;
			margin-top: -250rpx;
		}
		.introduce{
			font-size: 20rpx;
			position: absolute;
			top: 80rpx;
			right: 10rpx;
			
			
			max-width: 400rpx;  /*多长才会隐藏文字变成省略号*/
			overflow: hidden;
			display: -webkit-box; /** 对象作为伸缩盒子模型显示 **/
			-webkit-box-orient: vertical; /** 设置或检索伸缩盒对象的子元素的排列方式 **/
			-webkit-line-clamp: 3; /** 显示的行数 **/
		}
		.guide{
			font-size: 20rpx;
			position: absolute;
			bottom: 10rpx;
			right: 10rpx;
			
			
			max-width: 400rpx;  /*多长才会隐藏文字变成省略号*/
			overflow: hidden;
			display: -webkit-box; /** 对象作为伸缩盒子模型显示 **/
			-webkit-box-orient: vertical; /** 设置或检索伸缩盒对象的子元素的排列方式 **/
			-webkit-line-clamp: 3; /** 显示的行数 **/
		}
		
	}
	.wenzi{
		
	}
</style>
