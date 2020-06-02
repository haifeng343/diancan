<template>
	<view class="content">
		<view class="mtop">
			<view class="mtop-left">
				<view class="" v-if="detail.status ==1">订单已完成</view>
				<view class="" v-if="detail.status ==2">订单未完成</view>
				<view class="" v-if="detail.status ==3">订单已取消</view>
				<image class="right" src="../../static/img/right.png" mode=""></image>
			</view>
			<view class="orderCode">
				订单编号：{{detail.code}}
			</view>
		</view>
		<view class="list">
			<view class="item" v-for="item in detail.list" :key="item.id">
				<image class="img" :src="item.img" mode=""></image>
				<view class="content">
					<view class="top">
						<view class="name">
							{{item.name}}
						</view>
						<view class="money">
							{{item.money}}円
						</view>
					</view>
					<view class="bottom">
						菜品数量：{{item.number}}
					</view>
				</view>
			</view>
		</view>
		<view class="total">
			总计：{{total}}円
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				detail:{
					status:1,
					code:342435435324,
					list:[
						{
							id:1,
							name:'经典腓力牛排',
							img:'../../static/img/food1.png',
							money:10400,
							number:9
						},{
							id:2,
							name:'经典腓力牛排',
							img:'../../static/img/food2.png',
							money:1700,
							number:3
						},{
							id:3,
							name:'经典腓力牛排',
							img:'../../static/img/food4.png',
							money:12400,
							number:7
						},{
							id:4,
							name:'经典腓力牛排',
							img:'../../static/img/food1.png',
							money:13400,
							number:10
						},{
							id:5,
							name:'经典腓力牛排',
							img:'../../static/img/food2.png',
							money:9400,
							number:8
						},{
							id:6,
							name:'经典腓力牛排',
							img:'../../static/img/food4.png',
							money:21400,
							number:15
						},
					]
				}
			}
		},
		methods: {
			
		},
		onLoad() {
			let that = this;
			let tempArr = that.detail.list;
			let num = 0;
			tempArr.forEach(item=>{
				num += item.money
			})
			that.total = num;
		}
	}
</script>

<style lang="scss" scoped>
	uni-page-body{
		background-color: #F5F5F5;
	}
	.content{
		.mtop{
			width: 100%;
			height: 124rpx;
			display: flex;
			justify-content: space-between;
			align-items: center;
			box-sizing: border-box;
			padding: 0 40rpx;
			font-size: 32rpx;
			color: #333333;
			margin: 20rpx 0;
			background-color: #FFFFFF;
			.mtop-left{
				display: flex;
				justify-content: flex-start;
				flex-direction: row;
				align-items: center;
				.right{
					width: 14rpx;
					height: 24rpx;
					margin-left: 10rpx;
				}
			}
			.orderCode{
				font-size: 24rpx;
			}
		}
		.list{
			width: 100%;
			height: auto;
			display: flex;
			flex-direction: column;
			justify-content: flex-start;
			box-sizing: border-box;
			padding: 0 40rpx;
			background-color: #FFFFFF;
			.item{
				width: 100%;
				height: 170rpx;
				display: flex;
				align-items: center;
				justify-content: flex-start;
				flex-direction: row;
				box-sizing: border-box;
				border-bottom: 2rpx solid #EBEBEB;
				.img{
					width: 88rpx;
					height: 88rpx;
					margin-right: 20rpx;
				}
				.content{
					display: flex;
					flex:1;
					flex-direction: column;
					justify-content: space-around;
					font-size: 24rpx;
					color: #666666;
					.top{
						width: 100%;
						display: flex;
						justify-content: space-between;
						flex-direction: row;
						align-items: center;
						.name{
							color: #444444;
							font-size: 32rpx;
							line-height: 64rpx;
							font-weight: bold;
							width: 70%;
							overflow: hidden;
							text-overflow: ellipsis;
							white-space: nowrap;
						}
					}
				}
			}
		}
		.total{
			width: 100%;
			height: 100rpx;
			display: flex;
			align-items: center;
			background-color: #FFFFFF;
			justify-content: flex-end;
			box-sizing: border-box;
			padding-right: 40rpx;
			font-size: 32rpx;
			color: #444444;
			font-weight: bold;
			line-height: 64rpx;
		}
	}
</style>
