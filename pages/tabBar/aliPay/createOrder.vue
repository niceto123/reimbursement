<template>
	<view style="padding-top: 100rpx;position: relative;">
		<view class="orderTop">
			<uni-icons type="back" size="25" @click="back"></uni-icons> <text style="margin-left: 20rpx;font-size: 40rpx;line-height: 35rpx;">账单详情</text>
		</view>
		<view style="padding: 80rpx 20rpx 80rpx 20rpx;" class="contentBox">
			<view class="contentTop">
				<image class="vendorImg" style="background:transparent;" src="/static/tabBar/home.png"></image>
				<view style="margin-top: -20rpx;" class="textCenter">{{obj.vendorName || ''}}</view>
				<view class="textCenter" style="font-size: 60rpx;font-weight: 500;">-{{obj.num || ''}}</view>
				<view class="textCenter" style="margin-bottom: 30rpx;">交易成功</view>
				<view class="listLayout">
					<text style="color: #999;">付款方式</text> <text>{{obj.payment}}
						<uni-icons type="right" color="#999" size="15"></uni-icons>
					</text>
				</view>
				<view class="listLayout">
					<text style="color: #999;">支付宝积分</text>
					<view style="display: flex;align-items: center;background: #F4F9FF;border-radius:20rpx;padding: 5rpx 20rpx;">
						<image style="width: 30rpx;height: 30rpx;" src="/static/tabBar/vip.png"></image>
						<text style="margin-left: 10rpx;color: #1876F6;">立即领取10积分(已翻5倍)</text>
					</view>
				</view>
				<view class="listLayout">
					<text style="color: #999;">商品说明</text> <text>{{obj.goodsDescription}}
					</text>
				</view>
				<view class="listLayout">
					<text style="color: #999;">收单机构</text> <text>{{obj.acquirer}}
					</text>
				</view>
				<view class="listLayout">
					<text style="color: #999;">清算机构</text> <text>{{obj.cleaning}}
					</text>
				</view>
				<view class="listLayout">
					<text style="color: #999;">收款方全称</text> <text>{{obj.fullName}}
					</text>
				</view>
				<view class="listLayout">
					<text style="color: #999;">创建时间</text> <text>{{obj.createTime}}
					</text>
				</view>
				<view v-if="isMore" @tap="more" style="display: flex;justify-content: center;align-items: center;">
					<view style="color: #999;font-size: 30rpx;margin: 36rpx 0;">{{'更多 '}}
						<uni-icons type="bottom" color="#999" size="16"></uni-icons>
					</view>
				</view>
				<view v-else>
					<view class="listLayout">
						<text style="color: #999;">支付时间</text> <text>{{obj.payTime}}
						</text>
					</view>
					<view class="listLayout">
						<text style="color: #999;">订单号</text> <text>{{obj.order}}
						</text>
					</view>
					<view class="listLayout">
						<text style="color: #999;">商家订单号</text> <text>{{'商家可扫码退款或交易查询'}}
						</text>
					</view>
					<view style="display: flex;flex-direction: column;align-items: center;justify-content: center;">
						<view style="margin-top: 30rpx;" class="">
							<tki-barcode :val="obj.barCode" :opations="opations" />
						</view>
						<view style="color: #999;font-size: 20rpx;">{{obj.barCode.substr(0,4)}}'******点击查看订单号'
						</view>
					</view>

				</view>

			</view>
			<view class=" contentBottom ">
				<view class="blistLayout">
					<text >账单分类</text> <text style="color: #999;">{{'餐饮美食 '}}
						<uni-icons type="right" color="#999" size="15"></uni-icons>
					</text>
				</view>
				<view class="blistLayout">
					<text >标签和备注</text> <text style="color: #999;">{{'添加'}}
						<uni-icons type="right" color="#999" size="15"></uni-icons>
					</text>
				</view>
				<view class="blistLayout">
					<text >AA收款</text> <text style="color: #999;">
						<uni-icons type="right" color="#999" size="15"></uni-icons>
					</text>
				</view>
				<view class="blistLayout">
					<text >查看往来记录</text> <text style="color: #999;">
						<uni-icons type="right" color="#999" size="15"></uni-icons>
					</text>
				</view>
				<view class="blistLayout">
					<text >对此订单有疑问</text> <text style="color: #999;">
						<uni-icons type="right" color="#999" size="15"></uni-icons>
					</text>
				</view>
				<view class="blistLayout" style="border: 0 ;">
					<text >投诉</text> <text style="color: #999;">
						<uni-icons type="right" color="#999" size="15"></uni-icons>
					</text>
				</view>
			</view>
		</view>


	</view>
</template>

<script>
	import tkiBarcode from "@/components/tki-barcode/tki-barcode.vue"
	export default {
		data() {
			return {
				isMore: true,
				opations: {
					"displayValue": false
				},
				obj: {}
			};
		},
		onLoad: function(option) {
			// console.log(JSON.parse(option.obj))
			this.obj = JSON.parse(option.obj)
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
			}

		},
		components: {
			tkiBarcode
		}

	}
</script>

<style lang="scss">
	.textCenter {
		text-align: center;
		margin-top: 10rpx;
		padding: 0 20rpx;
	}

	.orderTop {
		display: flex;
		position: fixed;
		top: 0;
		z-index: 99;
		width: 100%;
		background-color: #FFFFFF;
		height: 100rpx;
		align-items: center;
		font-size: 30rpx;
		border-bottom: 1px solid #ddd;
	}

	.contentBox {
		position: relative;
		background: #F6F6F6;
		.contentBottom {
			background: #FFFFFF;
			padding: 0 10rpx 0;
			border-radius: 10rpx;
			margin-top: 20rpx;
			.blistLayout {
				display: flex;
				padding: 0 20rpx;
				justify-content: space-between;
				height: 100rpx;
				align-items: center;
				border-bottom: 1px solid #eee;
			}
		}
		.contentTop {
			background: #FFFFFF;
			padding: 0 10rpx 0;
			border-radius: 10rpx;

			.vendorImg {
				width: 90rpx;
				height: 90rpx;
				left: 50%;
				transform: translate(-50%,-40%);
				background-color: #eeeeee;
			}

			.listLayout {
				display: flex;
				align-items: center;
				justify-content: space-between;
				padding: 15rpx 20rpx 15rpx;
			}
		}
	}

	.testBorder {
		border: 1px solid red;
	}
</style>
