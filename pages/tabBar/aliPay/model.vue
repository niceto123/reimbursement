<template>
	<view style="margin-top: 80rpx;" class="">
		<view class="uni-list">
			<view class="btnLayout">
				<button class="mini-btn" type="primary" size="mini" @tap="cleanAll">清空历史记录</button>
			</view>
			<radio-group @change="radioChange">
				<label class="" v-for="(item, index) in items" :key="index">
					<view style="height: 70rpx;" class="btnFather">
						<radio :value="item.model" :checked="index === current" />
						<text>{{item.model}}</text> <text class="btn" style="right: 100rpx;" @tap="lookHistory(index)">选择</text> <text class="btn" @tap="deleteData(index)">删除</text>
					</view>

				</label>
			</radio-group>

		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				items: [],
				current: 0
			}

		},
		onLoad() {
			console.log('modelOnload', uni.getStorageSync('aliModel'))
			this.getHistory()
		},
		methods: {
			radioChange: function(evt) {
				for (let i = 0; i < this.items.length; i++) {
					if (this.items[i].value === evt.detail.value) {
						this.current = i;
						break;
					}
				}
			},
			cleanAll () {
				uni.removeStorageSync('aliModel')
				this.getHistory()
				
			},
			getHistory () {
			this.items = uni.getStorageSync('aliModel')
			},
			deleteData (index) {
				//删除历史记录
				let historyArr = uni.getStorageSync('aliModel')
				historyArr.splice(index,1)
				uni.setStorageSync('aliModel', historyArr)
				this.getHistory()
			},
			lookHistory (index) {
				//跳转页面
				let jsonStr = JSON.stringify(this.items[index])
				uni.navigateTo({
					url: '/pages/tabBar/aliPay/aliPay?obj=' + jsonStr
				})
				// uni.switchTab({
				// 	url: '/pages/tabBar/aliPay/aliPay?obj=' + jsonStr
				// });
				
			}
		}
	}
</script>

<style lang="scss">
	.listLayout,
	.uni-list-cell {
		height: 280px;
	}
	.btnFather {
		position: relative;
		.btn {
		display: block;
		position: absolute;
		top: 0;
		right: 0;
		padding: 0 20rpx 0;
		border:1rpx solid  blue ;
		border-radius: 10rpx;
	}
	}
	
</style>
