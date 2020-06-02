<template>
	<view class="content">
		<view class="mTop">
			<view class="m1">
				<view class="name">
					NNP牛排店（涩谷店)
				</view>
				<view class="imgs">
					<image src="../../static/img/search.png" @click="toSearch" mode=""></image>
					<image src="../../static/img/group.png" @click="toList" mode=""></image>
				</view>
			</view>
			<view class="txt">
				商家公告：周六~周末 9：00-22：00本店所有菜品均8折，其他分店不参与活动欢迎品尝
			</view>
		</view>
		<view class="group">
			<view class="group-left">
				<view class="item" v-for="item in groupLeft" @click="setShow(item.id)" :key="item.id" :class="[showId==item.id?'active':'']">
					{{item.name}}
				</view>
			</view>
			<view class="group-right">
				<view class="item" v-for="item in groupRight" :key="item.id">
					<image :src="item.img" class="img1" mode=""></image>
					<view class="item-content1">
						<view class="title">
							{{item.name}}
						</view>
						<view class="txt">
							{{item.txt}}
						</view>
						<view class="txt">
							{{item.price}}
						</view>
						<view class="mill">
							<view class="price">
								{{item.money}}円
							</view>
							<view class="computed">
								<image src="../../static/img/remove.png" v-if="item.number!==0" @click="changeTap(item.id,1)" class="img" mode=""></image>
								<input type="text" maxlength="3" :value="item.number" v-if="item.number!==0" class="input" />
								<image src="../../static/img/add.png" class="img" mode="" @click="changeTap(item.id,2)"></image>
							</view>
						</view>
					</view>
				</view>
			</view>
		</view>
		<view class="mask" :hover-stop-propagation="true" @click="isShowDialog = !isShowDialog" v-if="isShowDialog">
		</view>
		<view class="mask mask1" :hover-stop-propagation="true" v-if="isShowDialog1">
		</view>
		<view class="footer-content" v-if="isShowDialog && selectList.length>0">
			<view class="title">
				<view class="select">
					已选商品
				</view>
				<view class="clear" @click="clearCar">
					清空购物车
				</view>
			</view>
			<view class="list">
				<view class="item" v-for="item in selectList" :key="item.id">
					<view class="item-txt">
						<view class="txt1">
							{{item.name}}
						</view>
						<view class="txt2">
							{{item.total}}円
						</view>
					</view>
					<view class="computed">
						<image src="../../static/img/remove.png" v-if="item.number!==0" @click="changeTap1(item.id,1)" class="img" mode=""></image>
						<input type="number" maxlength="3" :value="item.number" @input="numChange(id)" v-if="item.number!==0" class="input" />
						<image src="../../static/img/add.png" class="img" mode="" @click="changeTap1(item.id,2)"></image>
					</view>
				</view>
			</view>
		</view>
		<view class="lastChild">
			
		</view>
		<view class="footer">
			<view class="number" v-if="total>0">
				{{total}}
			</view>
			<view class="footer-left">
				<image src="../../static/img/car.png" class="car" @click="showCar" mode=""></image>
				<view class="txt" v-if="totalMoney==0">
					快去下单吧
				</view>
				<view class="txt" v-else>
					{{totalMoney}}円
				</view>
			</view>
			<view class="btn" @click="toEat">点餐</view>
		</view>
		<!-- 删除确认弹窗 -->
		<view class="dialog-delete" v-if="isClear">
			<view class="dialog-title">
				清空购物车
			</view>
			<view class="dialog-content">
				确定要清空购物车？
			</view>
			<view class="dialog-footer">
				<view class="btn" @click="cancel">
					取消
				</view>
				<view class="btn" @click="sure">
					删除
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				showId: 1, //默认选择
				number: 1, //选择数量
				total: 0, //总数量
				totalMoney: 0, //总价格
				groupLeft: [{
					id: 1,
					name: '热卖商品'
				}, {
					id: 2,
					name: '优惠商品'
				}, {
					id: 3,
					name: '新品推荐'
				}, {
					id: 4,
					name: '美味牛排'
				}, {
					id: 5,
					name: '意大利面'
				}, {
					id: 6,
					name: '焗饭类'
				}, {
					id: 7,
					name: '小食甜品'
				}, {
					id: 8,
					name: '饮品类'
				}, {
					id: 9,
					name: '烧烤类'
				}, {
					id: 10,
					name: '口味选择'
				}, {
					id: 11,
					name: '餐具选择'
				}, {
					id: 12,
					name: '添加食材'
				}, ],
				groupRight: [{
					id: 1,
					img: '../../static/img/food1.png',
					name: 'NiuBi战斧牛排',
					txt: '配料：新鲜谷饲牛肉，口味一真的好香',
					price: '310G/块',
					money: 1300,
					number: 0,
				}, {
					id: 2,
					img: '../../static/img/food2.png',
					name: 'NiuBi西冷牛排',
					txt: '配料：新鲜谷饲牛肉，口味一真的好香',
					price: '1310G/块',
					money: 1700,
					number: 0,
				}, {
					id: 3,
					img: '../../static/img/food3.png',
					name: 'NiuBi神户牛肉',
					txt: '配料：新鲜谷饲牛肉，口味一真的好香',
					price: '3110G/块',
					money: 2100,
					number: 0,
				}, {
					id: 4,
					img: '../../static/img/food4.png',
					name: 'NiuBi和牛',
					txt: '配料：新鲜谷饲牛肉，口味一真的好香',
					price: '3310G/块',
					money: 7800,
					number: 0,
				}],
				selectList:[],//选中的列表
				isShowDialog:false,//mask
				isShowDialog1:false,//mask1
				isClear:false,//清除购物车确定弹窗
			}
		},
		methods: {
			setShow(id) {
				this.showId = id;
				this.groupRight = _.shuffle(this.groupRight);
			},
			//删除 添加
			changeTap(id, status) {
				let that = this;
				let num = 0;
				let totalMoney = 0;
				let tempArr = that.groupRight;
				tempArr.forEach(item => {
					if (item.id == id) {
						if (status == 1) {
							item.number--;
						} else {
							item.number++
						}
					};
					num += item.number;
					totalMoney += (item.number * item.money)
				})
				that.groupRight = tempArr;
				that.total = num;
				that.totalMoney = totalMoney;
			},
			//数值改变
			numChange(e,id){
				console.log(e,id);
				let tempArr = that.groupRight;
				tempArr.forEach(item => {
					if (item.id == id) {
						item.number = e.detail.value;
					};
				})
				that.groupRight = tempArr;
			},
			//显示购物车
			showCar(){
				let that = this;
				
				let tempArr = that.groupRight;
				let arr = [];
				arr = tempArr.filter(item=>{
					return (item.number!==0)
				})
				arr.forEach(item=>{
					item.total = (item.number * item.money);
				})
				that.selectList = arr;
				if(that.selectList.length==0){
					uni.showToast({
						title:'还未选择商品',
						icon:'none',
						duration:2000
					})
					return
				}
				that.isShowDialog = !that.isShowDialog;
			},
			//从购物车删除
			changeTap1(id, status) {
				let that = this;
				let num = 0;
				let totalMoney = 0;
				let tempArr = that.selectList;
				tempArr.forEach((item,index) => {
					if (item.id == id) {
						if (status == 1) {
							item.number--;
							if(item.number==0){
								tempArr.splice(index,1);
							}
						} else {
							item.number++
						}
					};
					num += item.number;
					totalMoney += (item.number * item.money)
				})
				if(tempArr.length==0){
					that.isShowDialog = false;
				}
				that.selectList = tempArr;
				that.total = num;
				that.totalMoney = totalMoney;
			},
			//清空购物车
			clearCar(){
				this.isClear = true;
				this.isShowDialog1 = true;
			},
			//清除购物车-确定
			sure(){
				let that = this;
				let tempArr =that.groupRight;
				tempArr.forEach(item=>{
					item.number = 0
				})
				that.groupRight = tempArr;
				that.selectList = [];
				that.total = 0;
				that.totalMoney= 0;
				that.isShowDialog = false;
				that.isShowDialog1 = false;
				that.isClear = false;
			},
			//清除购物车-取消
			cancel(){
				this.isClear = false;
				this.isShowDialog1 = false;
			},
			//点餐
			toEat(){
				uni.navigateTo({
					url:'../order/order'
				})
			},
			//订单列表
			toList(){
				uni.navigateTo({
					url:'../orderList/orderList'
				})
			},
			//搜索
			toSearch(){
				uni.navigateTo({
					url:'../search/search'
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
		flex: 1;
		flex-direction: column;
		.lastChild{
			width: 100%;
			height: 96rpx;
			background-color: transparent;
		}
		.mTop {
			width: 100%;
			height: auto;
			display: flex;
			align-items: center;
			flex-direction: column;
			font-size: 44rpx;
			line-height: 64rpx;
			box-sizing: border-box;
			padding: 0 26rpx;
			margin: 30rpx 0;

			.m1 {
				width: 100%;
				height: auto;
				display: flex;
				flex-direction: row;
				align-items: center;
				justify-content: space-between;

				.name {
					max-width: 70%;
					overflow: hidden;
					text-overflow: ellipsis;
					white-space: nowrap;
				}
			}

			.txt {
				font-size: 24rpx;
				color: #333333;
				line-height: 36rpx;
				margin-top: 22rpx;
			}

			.imgs {
				width: 20%;
				display: flex;
				flex-direction: row;
				justify-content: space-between;

				image {
					width: 36rpx;
					height: 36rpx;
				}
			}
		}

		.group {
			width: 100%;
			height: auto;
			display: flex;
			flex: 1;
			justify-content: space-between;
			.group-left {
				width: 160rpx;
				background-color: #F5F5F5;

				.item {
					width: 100%;
					height: 90rpx;
					display: flex;
					align-items: center;
					box-sizing: border-box;
					padding-left: 24rpx;
					font-size: 28rpx;
					color: #333333;
				}
			}

			.group-right {
				display: flex;
				flex: 1;
				flex-direction: column;
				justify-content: flex-start;

				.item {
					width: 93%;
					height: 240rpx;
					background: rgba(255, 255, 255, 1);
					box-shadow: 2px 2px 10px rgba(2, 54, 114, 0.09);
					border-radius: 10rpx;
					margin: 0 auto 20rpx;
					display: flex;
					justify-content: flex-start;
					flex-direction: row;

					.img1 {
						width: 158rpx;
						height: 158rpx;
						border-radius: 12rpx;
						margin: auto 32rpx;
					}

					.item-content1 {
						width: 300rpx;
						height: 178rpx;
						margin: auto 0;
						display: flex;
						flex-direction: column;
						justify-content: space-around;

						.title {
							width: 100%;
							overflow: hidden;
							text-overflow: ellipsis;
							white-space: nowrap;
							font-size: 32rpx;
							line-height: 64rpx;
							color: #444444;
						}

						.txt {
							font-size: 20rpx;
							color: #666666;
							line-height: 30rpx;
							width: 100%;
							overflow: hidden;
							text-overflow: ellipsis;
							white-space: nowrap;
						}

						.mill {
							width: 100%;
							height: auto;
							display: flex;
							align-items: center;
							justify-content: space-between;

							.price {
								display: flex;
								flex: 1;
								font-size: 28rpx;
								color: #FF531E;
								line-height: 60rpx;
							}

							.computed {
								width: 60%;
								height: auto;
								display: flex;
								align-items: center;
								justify-content: flex-end;

								.input {
									width: 70rpx;
									text-align: center;
								}

								.img {
									width: 42rpx;
									height: 42rpx;
								}
							}
						}
					}
				}
			}
		}
		.footer-content{
			width: 100%;
			display: flex;
			flex-direction: column;
			height: auto;
			max-height: 724rpx;
			overflow-y: scroll;
			background-color: #FFFFFF;
			position: fixed;
			bottom: 96rpx;
			box-sizing: border-box;
			padding: 0 40rpx;
			z-index: 2;
			.title{
				width: 100%;
				height: 130rpx;
				display: flex;
				align-items: center;
				justify-content: space-between;
				border-bottom:2rpx solid rgba(235,235,235,1);
				.select{
					position: relative;
					font-size: 36rpx;
					color: #444444;
					left: 30rpx;
				}
				.clear{
					font-size: 28rpx;
					color: #333333;
				}
			}
			.list{
				width: 100%;
				height: auto;
				display: flex;
				flex-direction: column;
				justify-content: flex-start;
				.item{
					width: 100%;
					height: 90rpx;
					display: flex;
					align-items: center;
					justify-content: space-between;
					font-size: 32rpx;
					color: #444444;
					.item-txt{
						width: 65%;
						height: auto;
						display: flex;
						justify-content: space-between;
						flex-direction: row;
						.txt1{
							width: 65%;
							overflow:hidden;
							text-overflow: ellipsis;
							white-space: nowrap;
						}
						.txt2{
							display: flex;
							flex: 1;
							justify-content: flex-end;
							text-align: right;
						}
					}
					.computed{
						width: 25%;
						display: flex;
						justify-content: flex-end;
						flex-direction: row;
						.img{
							width: 42rpx;
							height: 42rpx;
						}
						.input{
							width: 60rpx;
							text-align: center;
						}
					}
				}
			}
		}
		.footer {
			position: fixed;
			bottom: 0;
			left: 0;
			height: 96rpx;
			width: 100%;
			display: flex;
			align-items: center;
			flex-direction: row;
			justify-content: space-between;
			box-sizing: border-box;
			padding: 0 40rpx;
			font-size: 28rpx;
			z-index: 2;
			box-shadow: 0px 0px 8px rgba(2, 54, 114, 0.1);
			background-color: #FFFFFF;

			.footer-left {
				display: flex;
				flex-direction: row;

				.car {
					width: 50rpx;
					height: 42rpx;
				}

				.txt {
					font-size: 32rpx;
					color: #333333;
					margin-left: 96rpx;
				}
			}

			.btn {
				width: 200rpx;
				height: 60rpx;
				color: #fff;
				font-size: 28rpx;
				display: flex;
				align-items: center;
				justify-content: center;
				background: linear-gradient(180deg, rgba(252, 114, 63, 1) 0%, rgba(252, 94, 58, 1) 100%);
				box-shadow: 4rpx 4rpx 10rpx rgba(255, 138, 36, 0.3);
				border-radius: 32rpx;
			}

			.number {
				width: auto;
				padding: 0 16rpx;
				height: 42rpx;
				background: linear-gradient(180deg, rgba(252, 114, 63, 1) 0%, rgba(252, 94, 58, 1) 100%);
				border-radius: 25rpx;
				color: #FFFFFF;
				font-size: 28rpx;
				display: flex;
				align-items: center;
				justify-content: center;
				position: absolute;
				top: -21rpx;
				left: 10%;
			}
		}
		.dialog-delete{
			width:520rpx;
			height:320rpx;
			background:rgba(255,255,255,1);
			opacity:1;
			border-radius:20rpx;
			background-image: url(../../static/img/dialog.png);
			background-image: 100% 100%;
			z-index: 3;
			display: flex;
			justify-content: center;
			flex-direction: column;
			position: fixed;
			top: 50%;
			left: 50%;
			transform: translate(-50%,-50%);
			.dialog-title{
				font-size: 40rpx;
				color: #333333;
				font-weight: bold;
				line-height: 34rpx;
				margin: 60rpx auto 20rpx;
			}
			.dialog-content{
				color: #333333;
				font-size: 28rpx;
				line-height: 42rpx;
				text-align: center;
			}
			.dialog-footer{
				width: 80%;
				margin: 40rpx auto 0;
				height: auto;
				display: flex;
				justify-content: space-around;
				flex-direction: row;
				.btn{
					width:160rpx;
					height:60rpx;
					border:2rpx solid rgba(252,94,58,1);
					box-shadow:0 6rpx 12rpx rgba(253,93,57,0.2);
					border-radius:38rpx;
					font-size: 28rpx;
					color: #FC5E3A;
					display: flex;
					align-items: center;
					justify-content: center;
					
				}
				.btn:last-child{
					color: #fff;
					background:linear-gradient(180deg,rgba(252,119,65,1) 0%,rgba(254,71,51,1) 100%);
					box-shadow:0px 3px 6px rgba(253,93,57,0.2);
				}
				
			}
		}
	}

	.active {
		position: relative;
		color: #FC5E3A !important;
	}

	.active::after {
		content: '';
		position: absolute;
		width: 4rpx;
		height: 24rpx;
		top: 32rpx;
		left: 14rpx;
		background-color: #FC723F;
	}
	.select::after{
		content: '';
		position: absolute;
		width: 20rpx;
		height: 20rpx;
		left: -30rpx;
		top: 16rpx;
		background:linear-gradient(180deg,rgba(252,114,63,1) 0%,rgba(252,94,58,1) 100%);
		border-radius: 100%;
	}
</style>
