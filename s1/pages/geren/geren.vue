<template>
	<view class="big">
		<view class="box" v-if="isShow"  >
			<image   class="box-img" src="../../static/logo.png" mode=""   @click="denglu()" ></image>
			<view class="weidenglu" >未登录</view>
		</view>
		
		<!-- 上面if 下面else  未登录就是if，已登录就是else -->
		<view class="box" v-else>
			<image   class="box-img" src="../../static/logo.png" mode=""  ></image>
			<view class="weidenglu"  >已登录</view>
		</view>
		
		
		<view class="nav">
			<view class="nav-item">个人设置</view>
			<view class="nav-item">修改密码</view>
			<view class="nav-item">我的订单</view>
			<view class="nav-item1">意见反馈</view>
			
		</view>
		
		
		<!-- 退出的话直接取当前的反值 -->
		<button v-if="!isShow" @click="tuichu()" class="tuichu" >退出</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				token:"",
				
				// 给一个默认的值,true默认就是未登录状态
				isShow:true  
				
			};
		},
		
		// onShow每次判断token登录状态
		onShow() {
			this.token = uni.getStorageSync("token")
			this.istoken();
		},
		onLoad() {
			
		},
		methods: {
			denglu(){
				uni.navigateTo({
					url:"/pages/denglu/denglu"
				})
			},
			
			// token如果不是0,那token有值  那就是登录状态,isShow给false值,表示已经登录
			istoken(){
				if(this.token.length!=0){	//token长度为0
					this.isShow=false;	//是登录状态
				}else{
					
					// 反之则不是登录状态,true表示未登录
					this.isShow=true;
				}
			},
			
			// 退出登录按钮  固定格式
			tuichu(){
				uni.setStorage({
					key:"token",
					data:"",
					success: () => {
						this.token=uni.getStorageSync("token");
						this.istoken();
						
					}
				});
			}
		}
	}
</script>

<style lang="scss">
	.big{
		
	}
	.box{
		width: 200rpx;
		height: 200rpx;
		margin: 0 auto;
		margin-top: 100rpx;
		margin-bottom: 130rpx;
	}
	.box-img{
		border-radius: 100rpx;
		width: 200rpx;
		height: 200rpx;
		
	}
	.button{
		border: none;
	}
	.box2{
		margin-top: 30rpx;
	}
	.weidenglu, .ydenglu{
		font-size: 40rpx;
		margin-top: 30rpx;
		justify-content: center;
		text-align: center;
		margin-bottom: 20rpx;
	}
	.nav-item, .nav-item1{
		// margin-top: 20rpx;
		padding: 25rpx;
		font-size: 40rpx;
		border-top: 2rpx solid #999;
		// border-bottom:  2rpx solid #999;
	}
	.nav-item1{
		border-bottom:  2rpx solid #999;
	}
	.tuichu{
		width: 80%;
		margin-top: 40rpx;
	}
</style>
