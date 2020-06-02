<template>
	<view class="content">
		<image class="img" src="../../static/img/order.png" mode=""></image>
		<view class="title">
			点餐成功
		</view>
		<view class="txt">
			订单已提交，火热制作中
		</view>
		<view class="look" @click="toOrder">
			查看订单
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			toOrder(){
				uni.navigateTo({
					url:'../orderDetail/orderDetail'
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.content{
		width: 100%;
		height: auto;
		display: flex;
		flex-direction: column;
		justify-content: center;
		text-align: center;
		.img{
			width: 218rpx;
			height: 218rpx;
			margin: 152rpx auto 60rpx;
		}
		.title{
			font-size: 40rpx;
			color: #333333;
			font-weight: bold;
			line-height: 64rpx;
			margin-bottom: 10rpx;
		}
		.txt{
			font-size: 28rpx;
			color: #666666;
			line-height: 44rpx;
			margin-bottom: 40rpx;
		}
		.look{
			width:400rpx;
			height:76rpx;
			border:2rpx solid rgba(238,238,238,1);
			border-radius:38rpx;
			font-size: 32rpx;
			color: #666666;
			display: flex;
			align-items: center;
			justify-content: center;
			margin: 0 auto;
		}
	}
</style>
