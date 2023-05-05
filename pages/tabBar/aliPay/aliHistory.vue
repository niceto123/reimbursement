<template>
	<view style="margin-top: 80rpx;" class="">
		<view class="uni-list">
			<view class="btnLayout">
				<button class="mini-btn" type="primary" size="mini" @tap="cleanAll">清空历史记录</button>
			</view>
			<radio-group @change="radioChange">
				<label class="" v-for="(item, index) in items" :key="index">
					<view style="height: 70rpx;" class="btnFather">
						<radio :value="item.order" :checked="index === current" />
						<text>{{item.order}}</text> <text class="btn" style="right: 100rpx;" @tap="lookHistory(index)">查看</text> <text class="btn" @tap="deleteData(index)">删除</text>
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
			console.log('historyOnload', uni.getStorageSync('aliHistory'))
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
				uni.removeStorageSync('aliHistory')
				this.getHistory()
				
			},
			getHistory () {
			this.items = uni.getStorageSync('aliHistory')
			},
			deleteData (index) {
				//删除历史记录
				let historyArr = uni.getStorageSync('aliHistory')
				historyArr.splice(index,1)
				uni.setStorageSync('aliHistory', historyArr)
				this.getHistory()
			},
			lookHistory (index) {
				//跳转页面
				let jsonStr = JSON.stringify(this.items[index])
				uni.navigateTo({
					url: '/pages/tabBar/aliPay/createOrder?obj=' + jsonStr
				})
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
