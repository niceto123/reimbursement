<template>
	<view style="margin-top: 80rpx;">
		<view>
			<text>请输入店名：</text><input v-model="payContent.vendorName" class=" border" focus placeholder="填写商家名称" />
			<text>请输入支付金额：</text><input v-model="payContent.num" class=" border" placeholder="填写支付金额" />
			<text>请输入支付方式：</text><input v-model="payContent.payment" class=" border" placeholder="填写支付方式" />
			<text>请输入商品说明：</text><input v-model="payContent.goodsDescription" class=" border" placeholder="填写商品说明" />
			<text>请输入收单机构：</text><input v-model="payContent.acquirer" class=" border" placeholder="填写收单机构" />
			<text>请输入清算机构：</text><input v-model="payContent.cleaning" class=" border" placeholder="填写清算机构" />
			<text>请输入收款方全称：</text><input v-model="payContent.fullName" class=" border" placeholder="填写收款方全称" />
			<text>请输选择创建时间：</text>
			<uni-datetime-picker type="datetime" v-model="payContent.createTime" />
			<text>请输选择支付时间：</text>
			<uni-datetime-picker type="datetime" v-model="payContent.payTime" />
			<text>请输订单号：</text><input v-model="payContent.order" class=" border" placeholder="填写订单号(可不填,会根据创建时间生成)" />
			<text>请输入账单分类：</text><input v-model="payContent.categories" class=" border" placeholder="填写账单分类(可不填,会根据创建时间生成)" />
			<text>请输入模板名称：</text><input v-model="payContent.model" class=" border" placeholder="填写模板名称(可不填,但是保存模板时候建议填写)" />
		</view>
		<view class="btnLayout">
			<button class="mini-btn" type="primary" size="mini" @tap="gotoOrder">生成支付订单</button>
			<button class="mini-btn" type="primary" size="mini" @tap="saveModel">保存模板</button>
			<button class="mini-btn" type="primary" size="mini" @tap="findModel">查看模板</button>
			<button class="mini-btn" type="primary" size="mini" @tap="aliHistory">查看历史记录</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				payContent: {
					vendorName: '',
					num: '',
					payment: '',
					goodsDescription: '',
					acquirer: '',
					cleaning: '',
					fullName: '',
					createTime: '',
					payTime: '',
					order: '',
					barCode: '',
					categories: '',
					model: ''
				}
			};
		},
		onLoad(option) {
			// console.log('alipa--',option)
			if(option) {
				this.payContent = JSON.parse(option.obj)
			}
		},
		methods: {
			gotoOrder() {

				//添加历史记录
				let historyArr = uni.getStorageSync('aliHistory')
				historyArr = historyArr || []
				this.payContent.order = this.getOrderCode()
				this.payContent.barCode = this.getBarCode()
				historyArr.unshift(this.payContent)
				uni.setStorageSync('aliHistory', historyArr)
				//跳转页面
				let jsonStr = JSON.stringify(this.payContent)
				uni.navigateTo({
					url: '/pages/tabBar/aliPay/createOrder?obj=' + jsonStr
				})

			},
			aliHistory() {
				uni.navigateTo({
					url: '/pages/tabBar/aliPay/aliHistory'
				})
			},
			saveModel() {
				// uni.removeStorageSync('aliHistory')
				//保存模板
				let modelArr = uni.getStorageSync('aliModel')
				modelArr = modelArr || []
				modelArr.unshift(this.payContent)
				uni.setStorage({
					key: 'aliModel',
					data: modelArr,
					success: function () {
						uni.showToast({
							title: '模板添加成功',
							duration: 1000
						});
					}
				});

			},
			getOrderCode() {
				let finalOrder = ''
				if (!this.payContent.createTime) {
					var date = new Date();
					var month = date.getMonth() + 1;
					var strDate = date.getDate();
					if (month >= 1 && month <= 9) {
						month = "0" + month;
					}
					if (strDate >= 0 && strDate <= 9) {
						strDate = "0" + strDate;
					}
					finalOrder = date.getFullYear() + '' + month + strDate;
				} else {
					finalOrder = this.payContent.createTime.substr(0, 10).replace(/-/g, "")
				}
				for (let i = 0; i < 20; i++) {
					finalOrder = finalOrder + '' + Math.floor(Math.random() * 10)
				}
				return finalOrder
			},
			getBarCode() {
				let finalBar = ''
				for (let i = 0; i < 23; i++) {
					finalBar = finalBar + '' + Math.floor(Math.random() * 10)
				}
				return finalBar
			},
			findModel () {
				uni.navigateTo({
					url:'/pages/tabBar/aliPay/model'
				})
			}

		}
	}
</script>

<style lang="scss">
	.border {
		border: 1rpx solid black;
		border-radius: 10rpx;
		height: 50rpx;
	}

	.btnLayout {
		width: 100%;
		margin-top: 100rpx;
		display: flex;
		justify-content: center;
	}
</style>
