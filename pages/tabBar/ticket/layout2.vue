<template>
	<view>
		<view class="box">
			<view class="big-font" >{{obj.vendorName}}</view>
			<view style="font-size: 25rpx;margin: 10rpx auto;">
				【结账单】
			</view>
			<view class="">
				<view style="width: 70%;display: flex;justify-content: space-between;">
					<text>印单：{{obj.vendorName}}</text> <text>开单：{{obj.No}}</text>
				</view>
				<view style="width: 70%;display: flex;justify-content: space-between;">
					<text>台位：{{obj.tableNum}}</text> <text>人数：1</text>
				</view>
				<view style="width: 70%;display: flex;justify-content: space-between;">
					<text>时间：{{obj.payTime}}</text>
				</view>
			</view>

			<view class="line" style="margin:20rpx 0 5rpx ;"></view>
			<view class="line"></view>

			<view class="">
				<view class="foods">
					<view class="">
						出品
					</view>
					<view class="foods-num">
						<text class="width-33">
							数量
						</text>
						<text class="width-33">
							价格
						</text>
						<text class="width-33">
							金额
						</text>
					</view>
				</view>
				<view class="foods" v-for="(item, index) in obj.items">
					<view class="" v-if="item.name">
						{{item.name}}
					</view>
					<view class="foods-num" v-if="item.name">
						<text class="width-33">
							{{item.num}}
						</text>
						<text class="width-33">
							{{item.price}}
						</text>
						<text class="width-33">
							{{item.price*item.num}}
						</text>
					</view>
				</view>
				<view class="line" style="margin:20rpx 0 5rpx ;"></view>
				<view class="line"></view>
				<view class="foods">
					<view class="">
						消费金额：{{sum}}
					</view>
				</view>
				<view class="foods">
					<view class="" style="font-size: 40rpx;">
						应收金额：{{sum}}
					</view>

				</view>
			</view>

			<view class="line" style="margin:20rpx 0 5rpx ;"></view>
			<view class="line"></view>
			</view>
			<view class="text-align" style="font-size: 30rpx;">
				{{obj.vendorName}}欢迎您的下次光临!
			</view>
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
	}

	.text-align {
		text-align: center;

	}

	.big-font {
		font-size: 50rpx;
		margin: 20rpx auto;
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
				justify-content: space-between;
			}
		}
	}
</style>
