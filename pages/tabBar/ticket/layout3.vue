<template>
	<view>
		<view class="box">
			<view style="text-align: center;font-weight: 700;">{{obj.vendorName}}</view>
			<view style="font-size: 25rpx;margin: 10rpx auto;">
				客人就餐消费单
			</view>
			<text style="font-weight: 700;">桌号：{{obj.tableNum}}</text>
			<view class="line"></view>
			<view class="">
				<view style="width: 90%;display: flex;justify-content: space-between;">
					<text>日期：{{obj.payTime}}</text> <text>餐段：晚餐</text>
				</view>
				<view style="width: 90%;display: flex;justify-content: space-between;">
					<text>单号：{{obj.No}}</text> <text>服务方：{{obj.vendorName}}</text>
				</view>
			</view>
			<view class="foods">
				<view class="">
					菜品名称
				</view>
				<view class="foods-num">
					<text class="">
						数量
					</text>
					<text class="">
						小计
					</text>
				</view>
			</view>
			<view class="line">
			</view>
			<view class="">

				<view class="foods" v-for="(item, index) in obj.items">
					<view class="" v-if="item.name">
						{{item.name}}
					</view>
					<view class="foods-num" v-if="item.name">
						<text class="">
							{{item.num}}
						</text>
						<text class="">
							{{item.price*item.num}}
						</text>
					</view>
				</view>
				<view class="line">
				</view>

				<view class="foods" style="align-items: center;">
					<view class="" style="width: 65%;">
						折扣代码：
					</view>
					<view class="" style="width: 35%;">
						<view class="foods">
							消费合计：{{sum}}
						</view>
						<view class="foods">
							折扣金额：{{sum}}
						</view>
						<view class="foods">
							应收现金：{{sum}}
						</view>
					</view>
				</view>

			</view>
			<view class="" style="margin-top: 80rpx ;"></view>
			<view class="">打印时间：{{obj.payTime}}</view>
			<view class="">饮食通系统http://www.canyin.com.cn</view>

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
