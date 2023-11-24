<template>
	<view>
		<input type="text" placeholder="请输入用户名" v-model="user">
		<input type="password" placeholder="请输入密码" v-model="password">
		<view class="box">
			<button class="denglu"  type="primary" @click="clidenglu()">登录</button>
			<view class="zhuce" @click="zhuce()">点击注册</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				user:"",
				password:""
			}
		},
		onLoad() {
			this.token = uni.getStorageSync("token")
		},
		methods: {
			clidenglu(){
				uni.request({
					url:"http://124.93.196.45:10001/prod-api/api/login",
					data:{
						username:this.user,
						password:this.password
					},
					method:'POST',
					success: (res) => {
						uni.setStorage({
							key:"token",
							data:res.data.token,
						})
						console.log(res)
						uni.navigateBack()
						
						
						
					}
				})
			},
			zhuce(){
				uni.navigateTo({
					url:"/pages/zhuce/zhuce"
				})
			}
		}
	}
</script>

<style lang="scss">
	input{
		width: 90%;
		height: 80rpx;
		border: 2rpx solid #999;
		margin: 0 auto;
		margin-top: 30rpx;
		margin-bottom: 30rpx;
		text-align: center;
		border-radius: 30rpx;
	}
	.box{
		position: relative;
		.denglu{
			width: 90%;
			border-radius: 30rpx;
			border: 2rpx skyblue solid;
		}
		.zhuce{
			position: absolute;
			right: 10rpx;
			color: blue;
		}
	}
</style>
