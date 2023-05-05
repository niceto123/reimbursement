<template>
	<view>
		<view class="box">
			<view class="big-font">
				结账单-前台
			</view>
			<view class="big-font">{{obj.vendorName}}</view>
			<view class="line"></view>
			<view class="big-font">流水号：{{obj.No}}</view>
			<view class="">
				支付时间: {{obj.payTime}}
			</view>
			<view class="">
				收银员：{{obj.vendorName}}
			</view>
			<view class="">
				订单来源：收银机
			</view>
			<view class="line">
			</view>
			<view class="">
				<view class="foods">
					<view class="">
						菜品
					</view>
					<view class="foods-num">
						<text class="">
							数量
						</text>
						<text class="">
							单价
						</text>
					</view>	
				</view>
				<view class="foods" v-for="(item, index) in obj.items">
					<view class="" v-if="item.name">
						{{item.name}}
					</view>
					<view class="foods-num"  v-if="item.name">
						<text class="">
							{{item.num}}
						</text>
						<text class="">
							{{item.price}}
						</text>
					</view>	
				</view>
				<view class="foods">
					<view class="">
						合计
					</view>
					<view class="foods-num">
						<text class="">
							
						</text>
						<text class="">
							{{sum}}
						</text>
					</view>	
				</view>
				<view class="foods">
					<view class="">
						实付金额
					</view>
					<view class="foods-num">
						<text class="">	
						</text>
						<text class="">
							{{sum}}
						</text>
					</view>	
				</view>
			</view>

			<view class="line">
			</view>
			<view class="text-align">
				{{obj.vendorName}}
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				obj: {},
				sum:''
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
			getSum () {
				let item1 = this.obj.items[0]
				let item2 = this.obj.items[1]
				this.sum =  item1.price*item1.num + item2.price*item2.num
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
