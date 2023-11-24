<template>
	<view>
		<view class="all1">
			
			<view class="all-item1" v-for="(item,index) in all1" :key="index" @click="cliitem(item.id)">
				<image class="all-img1" :src="'http://124.93.196.45:10001'+item.imgUrl"  mode=""></image>
				<view class="all-text1">{{item.serviceName}}</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				all1:[]
			}
		},
		onLoad() {
			this.getAll1()
		},
		methods: {
			getAll1(){
				uni.request({
					url:"http://124.93.196.45:10001/prod-api/api/service/list",
					success: (res) => {
						this.all1 = res.data.rows
						console.log(res);
					}
				})
			},
			cliitem(id){
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
			}
		}
	}
</script>

<style lang="scss">
.all1{
		// width: 95%;
		// height: 300rpx;
		// background-color: skyblue;
		// margin-top: 20rpx;
		// border-radius: 30rpx;
		position: relative;
	}
	.all1{
		display: flex;
		flex-wrap: wrap;
		justify-content: space-evenly;
	}
	.all-item1{
		// margin-top: 100rpx;
		// background-color: purple;
		width: 150rpx;
		padding: 15rpx;
	}
	.all-img1{
		height: 130rpx;
		width: 130rpx;
	}
	.all-text1{
		// font-size: 17rpx;
		margin-left: -20rpx;
		text-align: center;
		colof: #999;
		
		max-width: 300rpx;  /*多长才会隐藏文字变成省略号*/
		overflow: hidden;
		display: -webkit-box; /** 对象作为伸缩盒子模型显示 **/
		-webkit-box-orient: vertical; /** 设置或检索伸缩盒对象的子元素的排列方式 **/
		-webkit-line-clamp: 1; /** 显示的行数 **/
		
		// 记住这五件套就行了
	}
</style>
