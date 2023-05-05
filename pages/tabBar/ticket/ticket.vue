<template>
	<view>
		<view>
			<text>请输入店名：</text><input v-model="payContent.vendorName" class=" border" focus placeholder="填写商家名称" />
			<view class="foodBox">	
			<text>菜品1：</text><input v-model="payContent.items[0].name" class=" border" placeholder="填写菜品" />
			<text>请输入单价：</text><input v-model="payContent.items[0].price" class=" border" placeholder="填写菜品单价" />
			<text>请输入数量：</text><input v-model="payContent.items[0].num" class=" border" placeholder="填写数量" />
			</view>
			
			<view class="foodBox">
			<text>菜品2：</text><input v-model="payContent.items[1].name" class=" border" placeholder="填写菜品" />
			<text>请输入单价：</text><input v-model="payContent.items[1].price" class=" border" placeholder="填写菜品单价" />
			<text>请输入数量：</text><input v-model="payContent.items[1].num" class=" border" placeholder="填写数量" />
			</view>

			<text>请输选择支付时间：</text>
			<uni-datetime-picker type="datetime" v-model="payContent.payTime" />
			<!-- <text>请输入模板名称：</text><input v-model="payContent.model" class=" border" placeholder="填写模板名称(可不填,但是保存模板时候建议填写)" /> -->
		</view>
		<view class="btnLayout">
			<button class="mini-btn" type="primary" size="mini" @tap="gotoOrder('')">生成模板一</button>
			<button class="mini-btn" type="primary" size="mini" @tap="gotoOrder(2)">生成模板二</button>
			<button class="mini-btn" type="primary" size="mini" @tap="gotoOrder(3)">生成模板三</button>
			<button class="mini-btn" type="primary" size="mini" @tap="gotoOrder(4)">生成模板四</button>
		<!-- 	<button class="mini-btn" type="primary" size="mini" @tap="saveModel">保存模板</button>
			<button class="mini-btn" type="primary" size="mini" @tap="findModel">查看模板</button>
			<button class="mini-btn" type="primary" size="mini" @tap="aliHistory">查看历史记录</button> -->
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				payContent: {
					vendorName: '',
					model: '',
					items:[
						{
							name:'',
							price:'',
							num: ''
						},
						{
							name:'',
							price:'',
							num: ''
						}
					],
					payTime:'',
					No:'',
					tableNum:'',
					machine:''
					
				}
			};
		},
		onLoad(option) {
			// console.log('alipa--',option)
			// if(option) {
			// 	this.payContent = JSON.parse(option.obj)
			// }
			this.getNo()
			this.getTableNum()
			this.getMachine()
		},
		methods: {
			gotoOrder(model) {
				//跳转页面
				let jsonStr = JSON.stringify(this.payContent)
				uni.navigateTo({
					url: '/pages/tabBar/ticket/layout'+ model +'?obj=' + jsonStr
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
				for (let i = 0; i < 16; i++) {
					finalBar = finalBar + '' + Math.floor(Math.random() * 10)
				}
				return finalBar
			},
			findModel () {
				uni.navigateTo({
					url:'/pages/tabBar/aliPay/model'
				})
			},
			getNo () {
				let finalBar = ''
				for (let i = 0; i < 2; i++) {
					finalBar = finalBar + '' + Math.floor(Math.random() * 10)
				}
				this.payContent.No = finalBar
				console.log(this.payContent.No);
			},
			getTableNum () {
				this.payContent.tableNum = this.randomNum(10,30)
			},
			getMachine () {
				this.payContent.machine = this.randomNum(2235,3015)
			}
			,
			randomNum(minNum,maxNum){ 
			    switch(arguments.length){ 
			        case 1: 
			            return parseInt(Math.random()*minNum+1,10); 
			        break; 
			        case 2: 
			            return parseInt(Math.random()*(maxNum-minNum+1)+minNum,10); 
			        break; 
			            default: 
			                return 0; 
			            break; 
			    } 
			} 
			

		}
	}
</script>

<style lang="scss">
	.foodBox {
		margin: 30rpx 0;
		border: 1px solid blue;
		border-radius: 30rpx;
		padding: 30rpx;
	}
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
