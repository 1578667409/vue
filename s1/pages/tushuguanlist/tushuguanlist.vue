<template>
	<view>
		<view class="name"></view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				tushuid:'',
				tushudata:''
			}
		},
		onLoad(e) {
			this.tushuid=e.id
			this.gettushuguanlist()
			// console.log(this.tushudata);
		},
		methods: {
			gettushuguanlist(){
				uni.request({
					
					url:'http://124.93.196.45:10001/prod-api/api/digital-library/library/'+this.tushuid,
					header:{
						Authorization:'eyJhbGciOiJIUzUxMiJ9.eyJsb2dpbl91c2VyX2tleSI6ImE1MzExYmVlLWRjYWUtNGFkZC1hNjNjLTlmZjU2ZTM4ODUyOSJ9.9J2Z2nZaw16SKdux4xqzPgs85DvRFubZFoHcbbRkpGs0XP87Mo84a88Oi4DaicwqOTMbYpPjfKEHM6cuSavG1g',
						},
					success: (res) => {
						this.tushudata=res.data.data
						console.log(res);
					}
				})
			}
		}
	}
</script>

<style>

</style>
