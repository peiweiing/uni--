<template>
	<view class="header bgccolor FX-sb FY-c">
			<view class="w3 FX-fs">
				<image class="img" src="../../static/img/payment_left.png" mode="" @tap="goback"></image>
			</view>
			<view class="w3 FX-c">
				<text class="" style="font-size: 16px;">{{title}}</text>
			</view>
			<view class="w3 FX-fe">
				<text>{{txt}}</text>
			</view>
	</view>
</template>

<script>
	export default {
		props: {
			imgUrl:String,
			title:String,
			txt:String,
			g_price:String,
			g_num:String
		},
		methods: {
			goback(){
				uni.navigateBack({
					delta: 1
				})
			},
			clickButton() {
				this.$emit("click")
			}
		}
	}
</script>

<style lang="scss" scoped>
	.header{
		height: 104rpx;
		color: #fff;
		padding:0 2%;
		.img{
			width: 50rpx;
			height: 50rpx;
		}
	}
	
</style>
