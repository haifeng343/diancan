<template>
	<view class="content">
		<view class="list">
			<view class="item" v-for="item in list" :key="item.id" @click="toDetail">
				<view class="title">
					<view class="txt1">
						{{item.name}}
					</view>
					<view class="txt2" v-if="item.status==1">订单已完成</view>
					<view class="txt2" v-if="item.status==2">订单未完成</view>
					<view class="txt2" v-if="item.status==3">订单已取消</view>
				</view>
				<view class="content1">
					<view class="txt1">
						<view class="">
							菜品数量：共{{item.number}}件菜品
						</view>
						<view class="">
							{{item.money}}円
						</view>
					</view>
					<view class="">
						下单时间：{{item.time}}
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list:[
					{
						id:1,
						name:'NNP牛排店（涩谷店)',
						status:1,
						number:10,
						money:9800,
						time:'2019/09/20  20:45'
					},{
						id:2,
						name:'NNP牛排店（涩谷店)',
						status:2,
						number:14,
						money:16800,
						time:'2019/09/21  20:42'
					},{
						id:3,
						name:'NNP牛排店（涩谷店)',
						status:3,
						number:16,
						money:20400,
						time:'2019/09/22  19:30'
					},{
						id:4,
						name:'NNP牛排店（涩谷店)',
						status:1,
						number:8,
						money:7800,
						time:'2019/09/23  18:35'
					},
				]
			}
		},
		methods: {
			toDetail(){
				uni.navigateTo({
					url:'../orderDetail/orderDetail'
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	uni-page-body{
		background-color: #F5F5F5;
	}
	.list{
		width: 100%;
		height: auto;
		.item{
			width: 96%;
			margin: 0 auto;
			height: 300rpx;
			box-sizing: border-box;
			padding: 0 40rpx;
			font-size: 24rpx;
			color: #333333;
			display: flex;
			flex-direction: column;
			background-color: #FFFFFF;
			border-radius: 10rpx;
			margin-top: 12rpx;
			.title{
				width: 100%;
				height: 130rpx;
				border-bottom:2rpx solid rgba(235,235,235,1);
				display: flex;
				justify-content: space-between;
				flex-direction: row;
				align-items: center;
				.txt1{
					font-size: 36rpx;
					color: #444444;
				}
			}
			.content1{
				width: 100%;
				display: flex;
				flex: 1;
				flex-direction: column;
				justify-content: center;
				line-height: 30rpx;
				.txt1{
					display: flex;
					justify-content: space-between;
					margin-bottom: 10rpx;
				}
			}
		}
		
	}
</style>
