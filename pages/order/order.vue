<template>
	<view class="content">
		<view class="list">
			<view class="item" v-for="item in orderList" :key="item.id">
				<image class="img" :src="item.img" mode=""></image>
				<view class="item-content">
					<view class="title">
						<view class="txt1">
							{{item.name}}
						</view>
						<view class="txt2">
							{{item.money}}円
						</view>
					</view>
					<view class="">
						菜品数量：{{item.number}}
					</view>
				</view>
			</view>
		</view>
		<view class="remark" @click="toRemark">
			<view class="">
				备注:<text>{{remark}}</text>
			</view>
			<image src="../../static/img/right.png" class="right" mode=""></image>
		</view>
		<view class="lastChild">
			
		</view>
		<view class="footer">
			<view class="txt1">
				{{total}}円
			</view>
			<view class="btn" @click="toPay">
				立即下单
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				orderList:[
					{
						id:1,
						name:'经典腓力牛排',
						money:2400,
						number:2,
						img:'../../static/img/food1.png'
					},{
						id:2,
						name:'A级和牛肉',
						money:4400,
						number:3,
						img:'../../static/img/food2.png'
					},{
						id:3,
						name:'顶级和牛',
						money:13400,
						number:2,
						img:'../../static/img/food4.png'
					},{
						id:4,
						name:'神户牛肉',
						money:24900,
						number:1,
						img:'../../static/img/food3.png'
					},
				],
				total:0,//总价格
				remark:'',//备注
			}
		},
		methods: {
			toRemark(){
				uni.navigateTo({
					url:'../remark/remark?remark='+this.remark
				})
			},
			toPay(){
				uni.navigateTo({
					url:'../orderSuccess/orderSuccess'
				})
			}
		},
		onLoad() {
			let that = this;
			let num = 0;
			let tempArr = that.orderList;
			tempArr.forEach(item=>{
				num+=item.money
			})
			that.total = num;
		}
	}
</script>

<style lang="scss" scoped>
	uni-page-body{
		background-color: #F5F5F5!important;
	}
	.content{
		
		.list{
			width: 100%;
			height: auto;
			display: flex;
			background: #FFFFFF;
			flex-direction: column;
			justify-content: flex-start;
			box-sizing: border-box;
			padding: 0 40rpx;
			.item{
				width: 100%;
				height: auto;
				display: flex;
				justify-content: space-between;
				padding: 40rpx 0;
				border-bottom: 2rpx solid rgba(235,235,235,1);
				.img{
					width: 88rpx;
					height: 88rpx;
					margin-right: 20rpx;
				}
				.item-content{
					display: flex;
					flex-direction: column;
					justify-content: flex-start;
					flex: 1;
					color: #333333;
					font-size: 24rpx;
					.title{
						width: 100%;
						height: auto;
						display: flex;
						align-items: center;
						justify-content: space-between;
						flex-direction: row;
						.txt1{
							font-size: 32rpx;
							color: #444444;
							line-height: 64rpx;
						}
					}
				}
			}
		}
		.remark{
			width: 100%;
			height: 124rpx;
			display: flex;
			align-items: center;
			justify-content: space-between;
			font-size: 32rpx;
			color: #333333;
			box-sizing: border-box;
			padding: 0 36rpx;
			margin-top: 20rpx;
			background-color: #FFFFFF;
			.right{
				width: 14rpx;
				height: 24rpx;
			}
		}
		.footer{
			width:100%;
			height:92rpx;
			background:rgba(255,255,255,1);
			box-shadow:0 0 16rpx rgba(2,54,114,0.1);
			position: fixed;
			bottom: 0;
			box-sizing: border-box;
			padding: 0 20rpx;
			display: flex;
			justify-content: space-between;
			flex-direction: row;
			align-items: center;
			.txt1{
				color: #FC5E3A;
				font-size: 44rpx;
				font-weight: bold;
			}
			.btn{
				width:200rpx;
				height:60rpx;
				background:linear-gradient(180deg,rgba(252,114,63,1) 0%,rgba(252,94,58,1) 100%);
				box-shadow:4rpx 4rpx 10rpx rgba(255,138,36,0.3);
				border-radius:32rpx;
				color: #FFFFFF;
				font-size: 28rpx;
				display: flex;
				align-items: center;
				justify-content: center;
			}
		}
		.lastChild{
			width:100%;
			height:92rpx;
			background: transperent;
		}
	}
</style>
