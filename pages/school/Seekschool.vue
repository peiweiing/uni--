<template>
	<view>
		
		<view class="module one FX-c">
			<view class="FX w100">
				<image class="img" src="../../static/images/index/search.png" mode=""></image>
				<input type="text" value="" placeholder="请输入学校名称"/>
			</view>
		</view>
		
		<view class="module two por">
			
			<view class="FX-sb">
				<view class="FY-c" @tap="show(1)">
					<text :class="isActive ? 'active' : ''">学校类型</text>
					<tui-icon name="arrowup" color="#007AFF" :size="16" v-if="isActive"></tui-icon>
					<tui-icon name="arrowdown" :size="16" v-else></tui-icon>
				</view>
				<view class="FY-c" @tap="show(2)">
					<text :class="poas ? 'active' : ''">所在地区</text>
					<tui-icon name="arrowup" color="#007AFF" :size="16" v-if="poas"></tui-icon>
					<tui-icon name="arrowdown" :size="16" v-else></tui-icon>
				</view>
				<view class="FY-c" @tap="show()">
					<tui-icon name="screen" :size="12" :color="sel ? '#007AFF' : '#333'" :bold="true"></tui-icon>
					<text :class="sel ? 'active' : ''">筛选</text>
				</view>
			</view>
			
			
			<view class="poa w100 pone" v-if="(isActive==true||poas==true)">
				<view class="FX" style="min-height: calc(80vh);">
					<view class="w3 FY" v-if="isActive">
						<view v-for="(v,i) in zhuanye" :key="i" :class="shows==i ? 'active' : ''" @tap="isshow(i)">{{v.txt}}</view>
					</view>
					<view class="w40 FY FY-c" v-if="poas">
						<view v-for="(v,i) in xueke" :key="i" :class="showss==i ? 'active' : ''" @tap="isshows(i)">{{v.txt}}</view>
					</view>
				</view>
			</view>
			
			<view class="poa w100 ptwo" v-if="sel">
				<view class="FY">
					<view class="w100 FY" style="min-height: calc(62vh);padding-top: 4%;">
						<view class="top" v-for="(v,i) in select">
							<text :class="sele==i? 'active' : ''" >{{v.name}}</text>
							<view class="FX-fs F-wrap">
								<!-- <view style="margin: 4% 6%;" v-for="(s,o) in select">{{s.name}}</view> -->
								<view style="margin: 4% 6%;" v-for="(s,o) in select" :class="sele==i&&seles==o ? 'active' : ''" @tap="issele(i,o)">{{s.name}}</view>
							</view>
						</view>
					</view>
					<view class="FX-sa end">
						<button class="w30" style="color: #999;" type="default" @tap="onreset">重置</button>
						<button class="w30 bgccolor" style="color: #fff;" type="default" @tap="onconfirm">确定</button>
					</view>
				</view>
			</view>
			
		</view>
		
		<view class="module three FX-sb FY-c" v-for="(v,i) in arrc">
			<view class="FY-c left">
				<image class="img" :src="v.img" mode=""></image>
				<view class="FY FX-sb">
					<text>{{v.txt}}</text>
					<view class="FX">
						<text>{{v.tab.tabs1}}</text>
						<text>{{v.tab.tabs2}}</text>
					</view>
				</view>
			</view>
			<view class="FY FY-fe right">
				<text>职业教育</text>
				<view class="FY-c">
					<image class="img" src="../../static/images/mall/my/icon_pingjia_3x.png" mode=""></image>
					<text style="font-size: 14px;">招生咨询</text>
				</view>
			</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				isActive:false,		//点击专业类别
				poas:false,		//点击门类学科
				sel:false,		//点击筛选
				shows:0,
				showss:0,
				sele:0,
				seles:0,
				arrc:[
					{img:'../../static/images/index/logo.png',txt:'清华大学',tab:{tabs1:'985',tabs2:'211'}},
					{img:'../../static/images/index/logo.png',txt:'清华大学',tab:{tabs1:'985',tabs2:'211'}},
					{img:'../../static/images/index/logo.png',txt:'清华大学',tab:{tabs1:'985',tabs2:'211'}},
					{img:'../../static/images/index/logo.png',txt:'清华大学',tab:{tabs1:'985',tabs2:'211'}},
					{img:'../../static/images/index/logo.png',txt:'清华大学',tab:{tabs1:'985',tabs2:'211'}},
				],
				zhuanye:[
					{txt:"哲学"},{txt:"美学"},{txt:"法学"},
				],
				xueke:[
					{txt:"政治"},{txt:"历史人文"},{txt:"法律咨询"},
				],
				select:[
					{
						name: '专业类型',
						isActive: false,
						list: ['管理专业','经济学专业','外国语文学类']
					},
					{
						name: '就读地区',
						isActive: false,
						list: ['管理专业','经济学专业','外国语文学类']
					},
					{
						name: '从业行业',
						isActive: false,
						list: ['管理专业','经济学专业','外国语文学类']
					},
					{
						name: '学历层次',
						isActive: false,
						list: ['管理专业','经济学专业','外国语文学类']
					},
				],
			}
		},
		onLoad: function(options) {
			
		},
		methods: {
			isshow(e){
				console.log(e);
				this.shows=e;
			},
			isshows(e){
				console.log(e);
				this.showss=e;
			},
			issele(e,s){
				console.log(e,s);
				this.sele=e;
				this.seles=s;
			},
			show(e){		//按钮切换筛选
				console.log(e);
				this.shows=0;this.showss=0;
				if(e==1){
					if(this.sel==true){
						this.sel=!this.sel
						this.isActive=!this.isActive
					}else if(this.isActive==true){
						this.poas=false
						this.isActive=false
					}else{
						this.isActive=!this.isActive
					}
				}else if(e==2){
					if(this.sel==true){
						this.sel=!this.sel
						this.poas=!this.poas
						this.isActive=!this.isActive
					}else if(this.isActive==true){
						this.poas=!this.poas
					}else{
						this.poas=!this.poas
						this.isActive=!this.isActive
					}
				}else{
					if(this.isActive==true||this.poas==true){
						this.poas=false
						this.isActive=false
						this.sel=!this.sel
					}else{
						this.sel=!this.sel
					}
				};
			},
			onreset(){
				this.sele=0;
				this.seles=0;
			},
			onconfirm(){
				
			}
		},
	}
</script>

<style>
	.bgccolor{background-color: #007AFF;}
	.module{
		margin: 2% 4%;
	}
	.one>view{
		padding: 2%;
		background-color: rgb(238,238,238);
		border-radius: 50rpx;
	}
	.one .img{
		width: 50rpx;
		height: 50rpx;
		margin: 1% 2%;
	}
	.one input{
		margin: 1% 1%;
	}
	.two{
		/* margin: 2% 0; */
		margin-top: 8%;
		margin-bottom: 4%;
		font-size: 16px;
	}
	.two .active{
		color: #007AFF;
	}
	.two .poa{
		background-color: rgba(213, 213, 213, 0.8);
		z-index: 9;
	}
	.two .poa .w3>view,.two .poa .w40>view{
		margin: 1rem 1%;
		width: 50%;
		text-align-last:justify;
		text-align:justify;
	}
	.two .poa>view>view{
		background-color: #fff;
	}
	.two .ptwo .end button{
		margin: 0;padding: 1% 0;line-height: normal;border-radius: 20rpx;
	}
	.two .ptwo .end button:first-child{
		border: 1px solid #999;
		background-color: #fff;
	}
	.two .ptwo .end button:first-child{
		/* bottom: 30px; */
	}
	.three{
		font-size: 16px;
		padding: 4% 0;
		border-bottom: 1px solid #1A1A1A;
	}
	.three .left{
		height: 100rpx;
	}
	.three .left>view{
		height: inherit;
		margin-left: 20rpx;
	}
	.three .left>view>view>text{
		border: 1px solid #1A1A1A;
		border-radius: 20rpx;
		padding: 0% 10%;
		margin-right: 20%;
	}
	.three .left .img{
		width: 100rpx;
		height: 100rpx;
		border-radius: 50%;
	}
	.three .right .img{
		width: 40rpx;
		height: 40rpx;
	}
	
	
	
</style>
