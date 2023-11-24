<template>
	<view>
		<form @submit="submit">
			<input type="text" name="user" placeholder="请输入用户名">
			<input type="password" name="password" placeholder="请输入密码">
			<input type="text" name="tel"  placeholder="请输入电话号码">
			
			
			<radio-group name="sex">
				<label>
					<radio value="0" /><text>男</text>
				</label>
				<label>
					<radio value="1" /><text>女</text>
				</label>
			</radio-group>
			<button type="primary" form-type="submit">立即注册</button>
		</form>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				obj:null,
			};
		},
		methods: {
			submit(e){
				this.obj=e.detail.value
				console.log(this.obj);
				uni.request({
					url:"http://124.93.196.45:10001/prod-api/api/register",
					data:{
						username:this.obj.user,
						password:this.obj.password,
						phonenumber:this.obj.tel,
						sex:this.obj.sex
					},
					method:'POST',
					success: (res) => {
						console.log(res.data.code);
						if(res.data.code==200){
							uni.navigateBack();
						}
						if(res.data.code==500){
							uni.showToast({
								title:'错误'
							})
						}
					}
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
	button {
		margin-top: 30rpx;
		width: 90%;
		border-radius: 30rpx;
	}
</style>
