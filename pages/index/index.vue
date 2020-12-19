<template>
	<view class="bgcimg main min-height">
		<view class="FX-c">
			<view class="F-xy search">
				<image class="img" src="../../static/images/index/search.png" mode=""></image>
				<input class="w40" type="text" placeholder="找学校 查专业" />
			</view>
		</view>
		
		<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000" class="swa">
			<swiper-item v-for="(v,i) in bannera" class="swipera">
				<view class="swiper-item">
					<image class="img" :src="v.img" mode=""></image>
				</view>
			</swiper-item>
		</swiper>
		
		<view class="FX-sa marg">
			<view class="FY FY-c btn" v-for="(v,i) in arra" @tap="nav(v.url,i)">
				<image class="img" :src="v.img" mode=""></image>
				<text>{{v.text}}</text>
			</view>
		</view>
		
		<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000" class="swb">
			<swiper-item v-for="(v,i) in bannerb" class="swiperb">
				<view class="swiper-item">
					<image class="img" :src="v.img" mode=""></image>
				</view>
			</swiper-item>
		</swiper>
		
		<view class="FX-sb FY-c moduleone marg">
			<view class="F-xy">
				<image class="img" src="../../static/images/my/feedback.png" mode=""></image>
				<text @tap="onnav(1)">问答</text>
			</view>
			<view class="F-xy">
				<image class="img" src="../../static/images/my/feedback.png" mode=""></image>
				<text @tap="onnav()">专题专区</text>
			</view>
		</view>
		<view class="moduletwo FX-sa FY-c">
			<image class="img" src="../../static/images/my/feedback.png" mode=""></image>
			<view class="FY FY-c w30">
				<text>在线客服</text>
				<text>有问题，找客服</text>
				<button class="w100" type="default" @tap="phone">立即咨询</button>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				arra:[
					{img:'../../static/img/rectangular_cxx.png',text:'查学校',url:"/pages/school/Seekschool"},
					{img:'../../static/img/rectangular_czy.png',text:'查专业',url:"/pages/school/Seekmajor"},
					{img:'../../static/img/rectangular_znxx.png',text:'个人测评',url:"/pages/user/Seekschool"},
					{img:'../../static/img/rectangular_znxzy.png',text:'智能选校',url:"/pages/index/AIselect"},
					{img:'../../static/img/rectangular_cxx.png',text:'智能选专业',url:"/pages/index/AIselect"},
				],
				bannera:[
					{img:'../../static/img/rectangular_hb.png'},
					{img:'../../static/img/rectangular_hb.png'},
					{img:'../../static/img/rectangular_hb.png'},
				],
				bannerb:[
					{img:'../../static/img/rectangular_lb.png'},
					{img:'../../static/img/rectangular_lb.png'},
					{img:'../../static/img/rectangular_lb.png'},
				]
			}
		},
		onLoad() {

		},
		methods: {
			phone(){
				uni.makePhoneCall({
				    phoneNumber: '400 123 1234' 
				});
			},
			nav(e,i){
				console.log(e,i)
				uni.navigateTo({
					url:e+"?id="+i
				})
			},
			onnav(e){
				if(e==1){
					uni.navigateTo({
						url:'/pages/index/Question'
					})
				}else{
					uni.navigateTo({
						url:'/pages/index/Subjectlist'
					})
				}
			}
		}
	}
</script>

<style>
	.main{
		padding: 0 5%;
	}
	.search{
		width: 100%;
		margin: 5% 0;
		padding: 2% 0;
		border-radius: 50rpx;
		background-color: rgb(238,238,238);
	}
	.search .img{
		width: 60rpx;
		height: 60rpx;
	}
	.marg{
		margin: 4% 0;
	}
	.btn .img{
		width: 120rpx;
		height: 120rpx;
	}
	.swa{
		height: 280rpx;
	}
	.swb{
		height: 180rpx;
	}
	.swipera{
		border-radius: 30rpx;
	}
	.swiperb{
		border-radius: 10rpx;
	}
	.swiper-item{
		height: 100%;
	}
	.swipera .img{
		width: 100%;
		height: inherit;
		border-radius: 30rpx;
	}
	.swiperb .img{
		width: 100%;
		height: inherit;
		border-radius: 10rpx;
	}
	.moduleone>view{
		width: 48%;
		height: 180rpx;
		border-radius: 10rpx;
	}
	.moduleone>view:first-child{
		background-color: #06AD56;
	}
	.moduleone>view:last-child{
		background-color: #007AFF;
	}
	.moduletwo{
		height: 240rpx;
		border-radius: 10rpx;
		box-shadow: 0 0 20rpx #ccc;
	}
	.moduleone .img{
		width: 100rpx;
		height: 100rpx;
	}
	.moduletwo .img{
		width: 120rpx;
		height: 120rpx;
	}
	.moduleone text{
		color: #fff;
	}
	.moduletwo text:first-child{
		font-size: 16px;
	}
	.moduletwo text:last-child{
		color: #999;
	}
	.moduletwo button{
		color: #fff;
		background-color: #007AFF;
		line-height: 100%;
		padding: 5%;
		border-radius: 40rpx;
	}
</style>
