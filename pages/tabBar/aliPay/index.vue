<template>
	<view style="margin-top: 80rpx;" class="">


		<button v-if="isLogin" class="mini-btn" type="primary" size="mini" @tap="gotoIndex">click to edit the aliPay</button>
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
				isLogin:false
			}
			
		},
		onLoad() {
			this.isLogin = uni.getStorageSync('isLogin')
		},
		methods: {
			gotoIndex () {
				uni.navigateTo({
					url: '/pages/tabBar/aliPay/aliPay'
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