<template>
	<view>
		<view class="top">
			<view class="top-item" v-for="(item,index) in top" :key="index" @click="cliitem(item)">
					<image class="item-img" :src="'http://124.93.196.45:10001'+item.imgUrl" mode="aspectFill"></image>
				<view class="item-wenzi">
					<view class="name">{{item.name}}</view>
					<view class="time">
						<view class="toptitle">营业时间:</view>
						<view class="businessHours">{{item.businessHours}}</view>
					</view>
					<view class="address">地址:{{item.address}}</view>
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
				top:[],
			}
		},
		onLoad() {
			this.gettop()
			console.log(this.top);
		},
		methods: {
			gettop(){
				uni.request({
					url:'http://124.93.196.45:10001/prod-api/api/digital-library/library/list',
					
					header:{
						Authorization:this.token
					},
					success: (res) => {
						this.top=res.data.rows;
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
			},
			cliitem(item){
				uni.navigateTo({
					url:`/pages/tushuguanlist/tushuguanlist?id=${item.id}`
				})
			}
		}
	}
</script>

<style lang="scss">
	
	.top {
		width: 95%;
		height: 300rpx;
		// background-color: red;
		margin: 0 auto;
		margin-top: 20rpx;
		.item-img{
			padding: 20rpx;
			border-radius: 50px;
			width: 260rpx;
			height: 260rpx;
		}
	}
	.top-item{
		background-color: #f3f3f3;
		display: flex;
		margin-top: 20rpx;
		border-radius: 30rpx;
	}
	.item-wenzi{
		display: flex;
		justify-content: space-between;
		flex-direction: column;
		flex: 1;
		// padding-left: 70rpx;
		margin-top: 20rpx;
		.name{
			font-size: 40rpx;
			font-family: '微软雅黑';
			font-weight: 700;
		}
		.address{
			font-size: 25rpx;
			margin-top: rpx;
		}
	}
	.businessHours{
		// 营业时间css样式
		margin-bottom: 10rpx;
		// margin-top: 10rpx;
	}
</style>
