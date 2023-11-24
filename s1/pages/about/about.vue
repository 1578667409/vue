<template>
	<view>
		<view class="img" v-for="(item,index) in img" :key="index">
			<image :src="'http://124.93.196.45:10001'+item.advImg" mode="aspectFill"></image>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				newsid:'',
				newsdata:''
			}
		},
		onLoad(e) {
			console.log(e);
			this.id=e.id
		},
		methods: {
			getalllist(){
				uni.request({
					url:'/prod-api/api/movie/rotation/list',
					success: (res) => {
						this.about=res.data.rows
						console.log(res)
					}
				})
			}
		}
	}
</script>

<style lang="scss">
	.img{
		width: 400rpx;
		height: 400rpx;
		background-color: red;
	}
</style>
