<template>
	<view>
		<view class="box">
			<view style="text-align: center;font-weight: 700;font-size: 60rpx;">{{obj.vendorName}}</view>
			<view class="line" style="margin:50rpx 0 10rpx ;"></view>
			<view class="line" style="margin-bottom: 60rpx;"></view>

			<view class="">
				<view style="width: 90%;display: flex;justify-content: space-between;">
					<text>日期：{{obj.payTime}}</text>
				</view>
				<view style="width: 90%;display: flex;justify-content: space-between;">
					<text>流水号：{{obj.No}}</text> <text>机号：{{obj.machine}}</text>
				</view>
				<view style="width: 90%;display: flex;justify-content: space-between;">
					<text>收款员：{{obj.machine}}</text> <text>餐台：{{obj.tableNum}}</text>
				</view>
			</view>
			<view class="line"></view>
			<view class="foods" style="margin: 10rpx 0;">
				<view class="">
					品名
				</view>
				<view class="foods-num">
					<text class="">
						数量
					</text>
					<text class="">
						单价
					</text>
					<text class="">
						金额
					</text>
				</view>
			</view>
			<view class="line">
			</view>
			<view class="" style="margin: 20rpx 0;">

				<view class="foods" v-for="(item, index) in obj.items">
					<view class="" v-if="item.name">
						{{item.name}}
					</view>
					<view class="foods-num" v-if="item.name">
						<text class="width-33">
							{{item.num}}
						</text>
						<text class="width-33">
							{{Number(item.price).toFixed(2)}}
						</text>
						<text class="width-33">
							{{Number(item.price*item.num).toFixed(2)}}
						</text>
					</view>
				</view>

			</view>
			<view class="line">
			</view>
			<view class="" style="font-size: 30rpx;margin-top: 30rpx">
				<view class="">
					应收：{{Number(sum).toFixed(2)}}
				</view>
				<view class="">
					实收：现金：{{Number(sum).toFixed(2)}}
				</view>
				<view class="">
					找零：0.00
				</view>
			</view>

			<view class="" style="margin-top: 80rpx ;"></view>
			<view class="" style="text-align:center;font-size:50rpx;">谢谢惠顾，欢迎再来</view>
			<view class="" style="margin-top: 15rpx ;"></view>
			<view class="" style="text-align:center;font-size:50rpx;">本小票仅限当日使用</view>

		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				obj: {},
				sum: ''
			};
		},
		onLoad: function(option) {
			console.log(JSON.parse(option.obj))
			this.obj = JSON.parse(option.obj)
		},
		mounted() {
			this.getSum()
		},
		methods: {
			back() {
				uni.navigateBack({
					delta: 1
				})
			},
			more() {
				this.isMore = !this.isMore
				// console.log(this.obj)
			},
			getSum() {
				let item1 = this.obj.items[0]
				let item2 = this.obj.items[1]
				this.sum = item1.price * item1.num + item2.price * item2.num
			}


		}

	}
</script>

<style lang="scss">
	.width-33 {
		width: 33%;
		text-align: center;
	}

	.text-align {
		text-align: center;

	}

	.big-font {
		font-size: 50rpx;
		margin: 20rpx 0;
	}

	.box {
		display: flex;
		flex-direction: column;
		padding: 40rpx;

		.line {
			border-bottom: 1px dashed black;
		}

		.foods {
			display: flex;
			justify-content: space-between;

			.foods-num {
				width: 300rpx;
				display: flex;
				justify-content: space-around;
			}
		}
	}
</style>
