<template>
	<view class="page bgccolor FY FY-c FX-sa por">
		<view class="w100 poa" style="top: 0;">
			<Head :title="title"></Head>
		</view>
		<view class="big" style="position: relative;">
			<view class="xian xone">
				<view class="dian done">
					
				</view>
			</view>
			<view class="xian xtwo">
				<view class="dian dtwo">
					
				</view>
			</view>
			<view class="xian xthree">
				<view class="dian dthree">
					
				</view>
			</view>
			<view class="xian xfour">
				<view class="dian dfour">
					
				</view>
			</view>
			<view class="F-xy big" style="font-size: 22px;">
				<swiper class="swiper F-xy poa" 
						circular="false"
						vertical="true"
						disable-touch="true"
						:autoplay="auto" 
						:interval="int" 
						:duration="dur"	>
						<swiper-item class="F-xy" v-if="eid==3" v-for="(v,i) in text" :key="i">
							<text>{{v.txt}}</text>
						</swiper-item>
						<swiper-item class="F-xy" v-if="eid==4" v-for="(v,i) in texts" :key="i">
							<text>{{v.txt}}</text>
						</swiper-item>
				</swiper>
				<!-- <swiper class="swiper F-xy poa" 
						circular="false"
						disable-touch="true"
						:autoplay="auto" 
						:interval="int" 
						:duration="dur"	>
						<swiper-item class="F-xy" v-if="eid==3&&auto" v-for="(v,i) in text" :key="i">
							<text>{{v.txt}}</text>
						</swiper-item>
						<swiper-item class="F-xy" v-if="eid==4&&auto" v-for="(v,i) in texts" :key="i">
							<text>{{v.txt}}</text>
						</swiper-item>
				</swiper> -->
			</view>
		</view>
		<view class="f-spacing">
			<text v-if="auto">正在分析···</text>
			<text v-else>已为您智能匹配到学校</text>
		</view>
	</view>
</template>

<script>
	import Head from '../../components/head/head.vue'
	export default {
		components:{
			Head
		},
		data() {
			return {
				eid:'',
				title:'',
				auto:true,
				int:500,
				dur:500,
				fun:null,
				text:[
					{txt:"学校1"},{txt:"学校2"},{txt:"学校3"},
					{txt:"西北大学1"},{txt:"科技大学2"},{txt:"师范大学3"},
					{txt:"工业大学1"},{txt:"科技大学2"},{txt:"师范大学3"},
				],
				texts:[
					{txt:'专业1'},
					{txt:'专业2'},
					{txt:'专业3'},
				]
			}
		},
		onLoad(e) {
			this.eid=e.id;
			var the = this;
			if(e.id==3){
				the.title="智能选学校";
				the.fun = setInterval(()=>{
					if(the.dur<3000){
						// the.int+=50;
						the.dur+=200;
						console.log("秒数++",the.int);
					}else if(the.dur>=3000){
						console.log('计时时间到');
						clearInterval(the.fun);
						the.auto=false;
					}
						console.log("秒数",the.int);
				},600)
			}else if(e.id==4){
				the.title="智能选专业";
				the.fun = setInterval(()=>{
					if(the.dur<3000){
						// the.int+=50;
						the.dur+=200;
						console.log("秒数++",the.int);
					}else if(the.dur>=3000){
						console.log('计时时间到');
						clearInterval(the.fun);
						the.auto=false;
					}
						console.log("秒数",the.int);
				},600)
			}
		},
		methods: {
			
		}
	}
</script>

<style>
	.page{
		color: #fff;
	}
	.big{
		height: 700rpx;width: 700rpx;
	}
	.swiper{
		font-size: 20px;
		width: 200rpx;height: 200rpx;
	}
	.xian{
		position: absolute;
		border-radius: 50%;
		border: 1px solid #fff;
		box-sizing: border-box;
		transition: all 2s; 
	}
	.dian{
		position: absolute;
		border-radius: 50%;
		background-color: #FFF;
		box-sizing: border-box;
		transition: all 2s; 
	}
	.xone,.xthree{
		animation:xone 8s infinite linear 0s;
	}
	.xtwo,.xfour{
		animation:xtwo 8s infinite linear 0s;
	}
	.done,.dthree{
		animation:done 4s infinite linear 0s;
	}
	.dtwo,.dfour{
		animation:dtwo 4s infinite linear 0s;
	}
	.xone{width: 100%;height: 100%;}
	.xtwo{width: 80%;height: 80%;top: 10%;left: 10%;}
	.xthree{width: 60%;height: 60%;top: 20%;left: 20%;}
	.xfour{
		width: 40%;height: 40%;top: 30%;left: 30%;
		border: 1px solid rgba(255,255,255,0.6);
		animation:xian 6s infinite linear 0s;
	}

	.done{width: 5%;height: 5%;left: 45%;top: -3%;}
	.dtwo{width: 5%;height: 5%;left: 45%;top: -3%;}
	.dthree{width: 5%;height: 5%;left: 45%;top: -3%;}
	.dfour{width: 5%;height: 5%;left: 45%;top: -3%;}
	@keyframes xian {
		0%{
			transform: rotate(360deg) scale(0.9);
			box-shadow: 2rpx 2rpx 40rpx #aaffff;
			color: rgba(255,255,255,0.4);
		}
		50%{
			transform: rotate(180deg) scale(1.1);
			box-shadow: 0rpx 0rpx 20rpx #fff;
			color: rgba(255,255,255,0.8);
		}
		100%{
			transform: rotate(0deg) scale(0.9);
			box-shadow: 2rpx 2rpx 40rpx #aaffff;
			color: rgba(255,255,255,0.4);
		}
	}
	@keyframes xone {
		0%{transform: rotate(0deg) ;}
		50%{transform: rotate(180deg) ;}
		100%{transform: rotate(360deg) ;}
	}
	@keyframes xtwo {
		0%{transform: rotate(360deg) ;}
		50%{transform: rotate(180deg) ;}
		100%{transform: rotate(0deg) ;}
	}
	@keyframes done {
		0%{
			transform: scale(0.8);
			box-shadow: 0 0 40rpx #ff0000;
		}
		50%{
			transform: scale(1.2);
			box-shadow: 0 0 40rpx #640000;
		}
		100%{
			transform: scale(0.8);
			box-shadow: 0 0 40rpx #ff0000;
		}
	}
	@keyframes dtwo {
		0%{
			transform: scale(1.5);
			box-shadow: 0 0 40rpx #ff0004;
		}
		50%{
			transform: scale(1);
			box-shadow: 0 0 40rpx #900002;
		}
		100%{
			transform: scale(1.5);
			box-shadow: 0 0 40rpx #ff0004;
		}
	}
</style>
