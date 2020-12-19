<template>
	<view>
		<view class="and-div FX-sa">
			<text @tap="tit=i" :class="tit==i? 'active' : ''" v-for="(v,i) in title">{{v}}</text>
		</view>
		<hr/>
		<view class="end-div">
			<view class="div FX-sb" v-if='img.length>4'>
				<view class="divcs w50 FY FX-sb">
					<text class="f-hidden text">以联合带创新 以共建促自建</text>
					<view class="FX-sb">
						<text>1k阅读</text>
						<text>2020-10-11 16:33:29</text>
					</view>
				</view>
				<image class="img" src="../../static/images/index/logo.png" mode=""></image>
			</view>
			<view class="div FX-sb" v-if='img.length<4'>
				<view class="divcs FY FX-sb">
					<text class="f-hidden">以联合带创新 以共建促自建</text>
					<view class="">
						<image class="imgcs" src="../../static/images/index/logo.png" mode=""></image>
						<image class="imgcs" src="../../static/images/index/logo.png" mode=""></image>
						<image class="imgcs" src="../../static/images/index/logo.png" mode=""></image>
					</view>
					<view class="FX-sb w70">
						<text>1k阅读</text>
						<text>2020-10-11 16:33:29</text>
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
				tit:'',
				title:['推荐','助力高考','名师讲堂','专业咨询','高职单招'],
				img:[
					'../../static/images/index/logo.png',
					'../../static/images/index/logo.png',
					'../../static/images/index/logo.png',
				]
			}
		},
		methods: {
			
		}
	}
</script>

<style lang="scss" scoped>
	.active{
		color: #007AFF;
		border-bottom: 1px solid #007AFF;
	}
	.and-div{
		font-size: 14px;
		padding: 4% 0;
		/* border-bottom: 1px solid #999; */
	}
	.end-div{
		font-size: 14px;
		.div{
			margin: 0 4%;
			padding: 4% 0;
			border-bottom: 1px solid #999;
			.divcs .text{
				text-align-last:justify;
				text-align:justify;
			}
			.divcs>view>text{
				font-size: 12px;
			}
			.img{
				width: 180rpx;height: 120rpx;
			}
			.imgcs{
				width: 180rpx;height: 200rpx;
				margin: 2% 4rpx;
			}
		}
	}
</style>
