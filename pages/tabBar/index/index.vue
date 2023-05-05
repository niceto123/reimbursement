<template>
	<view>
		<button v-if="isLogin" @tap="btn">click to edit the ticket</button>
		<view v-else class="">
			<text>宇宙第一帅？</text>
			<input v-model="content" class=" border" placeholder="请输入答案" />
			<button class="border" @tap="submit">confirm</button>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				isLogin:true,
				content:''
			};
		},
		onLoad() {
			// this.isLogin = uni.getStorageSync('isLogin')
		},
		methods: {
			btn () {
				uni.navigateTo({
					url:'/pages/tabBar/ticket/ticket'
				})
			},
			submit () {
				if(this.content == 'hzj') {
					uni.setStorageSync('isLogin', true)
					uni.showToast({
						title:'退出重开',
						duration: 2000
					})
				}else {
					uni.showToast({
						title:'the answer is wrong',
						duration: 2000
					})
				}
			}
		}
	}
</script>

<style lang="scss">
.border {
	border: 1px solid black;
	border-radius:20rpx ;
}
</style>
