<template>
	<view class="content">
		<image src="../../static/img/indexBg.png" class="bgImg" mode=""></image>
		<view class="mtop">
			<image src="../../static/img/logo.png" class="logo" mode=""></image>
			<view class="txt1">
				NNP牛排店
			</view>
		</view>
		<view class="welcome">
			欢迎光临，ColorWoof！
		</view>
		<view class="mBom">
			<view class="title">
				请问您几位？
			</view>
			<view class="number">
				桌台：002
			</view>
			<view class="list">
				<view class="show" v-if="show">
					<view class="item" v-for="item in items" @click="setShow(item.id)" :key="item.id" :class="[item.id==showId?'active':'']">
						{{item.name}}
					</view>
				</view>
				<view class="show" v-else>
					<view class="item" v-for="item in items1" @click="setShow(item.id)" :key="item.id" :class="[item.id==showId?'active':'']">
						{{item.name}}
					</view>
					<view class="item item1">
						<input type="number" class="input" :value="number" maxlength="2" @input="inputChange"/>
						<text>人</text>
					</view>
				</view>
			</view>
			<button class="btn" @click="goToGroup">开始点餐</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				items: [{
					id: 1,
					name: '1人'
				}, {
					id: 2,
					name: '2人'
				}, {
					id: 3,
					name: '3人'
				}, {
					id: 4,
					name: '4人'
				}, {
					id: 5,
					name: '5人'
				}, {
					id: 6,
					name: '6人'
				}, {
					id: 7,
					name: '7人'
				}, {
					id: 8,
					name: '更多'
				}],
				items1: [{
					id: 1,
					name: '1人'
				}, {
					id: 2,
					name: '2人'
				}, {
					id: 3,
					name: '3人'
				}, {
					id: 4,
					name: '4人'
				}, {
					id: 5,
					name: '5人'
				}, {
					id: 6,
					name: '6人'
				}, {
					id: 7,
					name: '7人'
				}],
				showId: 1, //默认选择
				show:true,//默认展示
				number:'',//多少人
			}
		},
		onLoad() {
			let that = this;
		},
		methods: {
			setShow(id) {
				this.showId = id;
				if (this.showId !== 8) {
					this.show=true;
				}else{
					this.show =false;
				}
			},
			inputChange(e){
				this.number = e.detail.value;
			},
			goToGroup(){
				uni.navigateTo({
					url:'../group/group'
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.content {
		width: 100%;
		height: 100%;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		position: relative;
		.bgImg{
			width: 100%;
			height: 100%;
			position: fixed;
			top: 0;
			left: 0;
			z-index: 1;
		}
		.mtop {
			width: 100%;
			height: auto;
			display: flex;
			justify-content: center;
			align-items: center;
			margin-top: 164rpx;
			margin-bottom: 112rpx;
			z-index: 2;
			.logo {
				width: 120rpx;
				height: 120rpx;
			}

			.txt1 {
				color: #FFFFFF;
				font-size: 52rpx;
				position: relative;
				left: 30rpx;
				line-height: 64rpx;
				z-index: 1;
			}
		}

		.welcome {
			width: 100%;
			text-align: center;
			font-size: 40rpx;
			color: #FFFFFF;
			line-height: 44rpx;
			margin-bottom: 60rpx;
			z-index: 2;
		}

		.mBom {
			z-index: 2;
			width: 702rpx;
			height: 584rpx;
			margin: 0 auto;
			display: flex;
			flex-direction: column;
			background: rgba(255, 255, 255, 1);
			border-radius: 10rpx;

			.title {
				font-size: 40rpx;
				color: #333333;
				line-height: 64rpx;
				margin: 60rpx auto 10rpx;
			}

			.number {
				color: #333333;
				font-size: 28rpx;
				line-height: 64rpx;
				text-align: center;
				margin-bottom: 48rpx;
			}

			.list {
				width: 90%;
				height: auto;
				display: flex;
				margin: 0 auto;
				justify-content: flex-start;
				flex-wrap: wrap;

				.show {
					width: 100%;
					height: auto;
					display: flex;
					margin: 0 auto;
					justify-content: flex-start;
					flex-wrap: wrap;

					.item {
						width: 25%;
						height: 76rpx;
						display: flex;
						align-items: center;
						font-size: 36rpx;
						line-height: 44rpx;
						justify-content: center;
						position: relative;
						.input{
							width: 36rpx;
							font-size: 36rpx;
						}
					}
				}

			}

			.btn {
				width: 400rpx;
				height: 92rpx;
				background: linear-gradient(180deg, rgba(252, 114, 63, 1) 0%, rgba(252, 94, 58, 1) 100%);
				border-radius: 46rpx;
				color: #FFFFFF;
				font-size: 36rpx;
				line-height: 44rpx;
				display: flex;
				align-items: center;
				justify-content: center;
				margin-top: 40rpx;
			}
		}
	}

	.active {
		background: linear-gradient(180deg, rgba(252, 114, 63, 1) 0%, rgba(252, 94, 58, 1) 100%);
		border-radius: 38rpx;
		color: #FFFFFF;
	}
	.item1::before{
		content: '';
		position: absolute;
		width: 80rpx;
		height: 1rpx;
		background: #999999;
		bottom: 10rpx;
		left: 25%;
	}
</style>
