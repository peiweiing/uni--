<template>
	<view class="page">
		<view class="FX-sa and-div">
			<text @tap="oncut=1" class="f-bold" :class="oncut==1? 'active' : ''">问题分类</text>
			<text @tap="oncut=2" class="f-bold" :class="oncut==2? 'active' : ''">我要提问</text>
		</view>
		<view v-if="oncut==1">
			<view class="one boxcolor" v-for="(v,i) in arr">
				<view class="FY-c">
					<image class="img" src="../../static/components/bottom-navigation/icon_menu_gray.png" mode=""></image>
					<text class="f-bold f-hidden w50">{{v.txt}}</text>
				</view>
				<view class="FY-c">
					<image class="img" src="../../static/components/bottom-navigation/icon_menu_gray.png" mode=""></image>
					<text class="f-bold f-hidden w70">{{v.txts}}</text>
				</view>
				<view class="FX-sb end">
					<view class="FY-c">
						<image class="imgcs" src="../../static/components/scroll-top/icon_index_3x.png" mode=""></image>
						<text>CC老师的回答</text>
					</view>
					<text>回答{{v.num}}</text>
				</view>
			</view>
		</view>
		<view class="two" v-if="oncut==2">
			<view class="twoing">
				<view class="FY-c">
					<image class="imgcs" src="" mode=""></image>
					<text>CC老师</text>
				</view>
				<textarea value="" placeholder="" />
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				oncut:1,
				arr:[
					{txt:"大学专业时，发现。。。",txts:"不要再专业报考模块里抖机灵。。。",num:'24'},
					{txt:"大学专业时，发现。。。",txts:"不要再专业报考模块里抖机灵。。。",num:'24'},
				]
			}
		},
		methods: {
			
		}
	}
</script>

<style>
	.active{
		color: #007AFF;
		border-bottom: 1px solid #007AFF;
	}
	.and-div{
		padding: 4% 0;
		background-color: #fff;
	}
	.and-div text{
		font-size: 18px;
		padding-bottom: 2%;
	}
	.one{
		font-size: 16px;
		padding: 4%;
		margin: 4%;
		border-radius: 10rpx;
		background-color: #fff;
	}
	.one .end{
		font-size: 14px;
		color: #999;
		margin-top: 10%;
	}
	.two{
		min-height: calc(90vh);
		font-size: 14px;
		color: #999;
		background-color: #fff;
	}
	.two .twoing{
		margin: 0 4% 4%;
		padding: 4%;
		border-radius: 20rpx;
		background-color: #eee;
	}
	
	.img{
		width: 80rpx;height: 80rpx;border-radius: 10rpx;
	}
	.imgcs{
		width: 40rpx;height: 40rpx;border-radius: 50%;
	}
</style>
