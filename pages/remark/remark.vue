<template>
	<view class="content">
		<textarea :value="txt" class="txt" @input="setTxt" maxlength="20" placeholder="请输入备注内容" />
		<view class="btn" @click="send">
			确定
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				txt:'',//备注内容
			}
		},
		methods: {
			setTxt(e){
				this.txt = e.detail.value;
			},
			send(){
				let pages = getCurrentPages();
				let befoPage = pages[pages.length-2];
				befoPage.remark = this.txt;
				uni.navigateBack({
					delta:1
				})
			},
		},
		onLoad(options) {
			this.txt = options.remark;
		},
	}
</script>

<style lang="scss" scoped>
	.content{
		.txt{
			width: 90%;
			height: 200rpx;
			border-radius: 16rpx;
			font-size: 28rpx;
			color: #333333;
			margin: 20rpx auto;
			box-sizing: border-box;
			padding: 20rpx;
			border: 1rpx solid #EBEBEB;
		}
		.btn{
			width: 80%;
			margin: 30rpx auto;
			height:80rpx;
			font-size: 28rpx;
			color: #FFFFFF;
			border-radius: 16rpx;
			display: flex;
			justify-content: center;
			align-items: center;
			background:linear-gradient(180deg,rgba(252,114,63,1) 0%,rgba(252,94,58,1) 100%);
		}
	}
</style>
