<template>
	<view>
		<view class="box">
			<view class="title">{{newsData.title}}</view>
			
			<view class="time">
				<text>发布时间：</text><text>{{newsData.createTime}}</text>
			</view>
			
			<view class="content">
				<rich-text :nodes="newsData.content"></rich-text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				newsId:"",
				newsData:"",
			}
		},
		onLoad(e) {
			this.newsId=e.id;
			this.getNews();
		},
		methods: {
			getNews(){
				uni.request({
					url:"http://124.93.196.45:10001/prod-api/press/press/"+this.newsId,
					success: (res) => {
						this.newsData = res.data.data;
					}
				})
			}
		}
	}
</script>

<style lang="scss">
	.title{
		padding: 20rpx;
		text-align: center;
		font-size: 60rpx;
	}
	.time{
		justify-content: space-between;
		padding: 10rpx;
		background-color: #999;
		width: 90%;
		margin: 0 auto;
	}
	.content{
		padding: 20rpx;
		text-align: center;
		font-size: 36rpx;
	}
</style>
