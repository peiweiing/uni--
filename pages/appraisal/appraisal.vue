<template>
	<view>
		<view id="top-box" class="cu-bar bg-white bottoms solid-bottom">
			<view class="action text-black exam-types">
				<text v-if="currentType===1">判断题</text>
				<text v-else-if="currentType===2">单选题</text>
				<text v-else-if="currentType===3">多选题</text>
				<text v-else-if="currentType===4">填空题</text>
				<text v-else-if="currentType===5">问答题</text>
			</view>
			<!-- 题目进度 -->
			<view class="progress">
				<text>{{pageIndex}}</text>
				<text>/{{subjectList.length}}</text>
			</view>
			<view class="action exam-card">
				<button class="cu-btn bg-green shadow" @tap="showCardModal" data-target="modalCard">答题卡</button>
			</view>
		</view>
		<view class="cu-modal" :class="modalCard=='modalCard'?'show':''" @tap="hideCardModal">
			<view class="cu-dialog" @tap.stop>
				<scroll-view class="page padding" :scroll-y=true :style="{'height':swiperHeight}">
					<view class="cu-bar solid-bottom">
						<view class="action">
							<text class="cuIcon-title text-red"></text>答题卡
						</view>
					</view>
					<!-- 选择题目 -->
					<view class="grid col-5 ">
						<view class="margin-tb-sm text-center" v-for="(subject,index) in subjectList" :key="index">
							<button class="cu-btn round" :class="[subject.userAnswer.length===0?'line-grey':'bg-red']" @click="assignSubject(index)">{{index+1}}</button>
						</view>
					</view>
				</scroll-view>
			</view>
		</view>
		<!-- 提交试题纠错部分 -->
		<view class="cu-modal padding " :class="modalError=='modalError'?'show':''" @tap="hideErrorModal">
			<view class="cu-dialog bg-white" @tap.stop>
				<view class="cu-bar solid-bottom ">
					<view class="action">
						<text class="cuIcon-title text-red"></text>试题纠错
					</view>
				</view>
				<radio-group class="block">
					<view class="cu-list menu text-left">
						<view class="cu-item cu-item-error" v-for="error in errorList" :key="index">
							<radio :value="error"></radio>
							<view class="title text-black margin-left">{{error}}</view>
						</view>
					</view>
				</radio-group>
				<view class="padding flex flex-direction ">
					<button class="cu-btn bg-red margin-tb-sm lg" @click="SubmitError">提 交</button>
				</view>
			</view>
		</view>
		<form>
			<swiper :current="subjectIndex" class="swiper-box" @change="SwiperChange" :style="{'height':swiperHeight}">
				<swiper-item v-for="(subject,index) in subjectList" :key="index">
					<view v-if="index-subjectIndex>=-1&&index-subjectIndex<=1">
						<scroll-view scroll-y="true">
							<view id="desc">
								这里是对一些题目的解释这里是对一些题目的解释这里是对一些题目的解释
								这里是对一些题目的解释这里是对一些题目的解释这里是对一些题目的解释
								这里是对一些题目的解释这里是对一些题目的解释这里是对一些题目的解释
								这里是对一些题目的解释这里是对一些题目的解释这里是对一些题目的解释
								这里是对一些题目的解释这里是对一些题目的解释这里是对一些题目的解释
								这里是对一些题目的解释这里是对一些题目的解释这里是对一些题目的解释
							</view>
						</scroll-view>
						<!-- 题目类型 -->
						<view class="cu-bar bg-white solid-bottom">
							<view class="action text-black">
								<text class="cuIcon-title text-red"></text>{{subject.title}}
							</view>
						</view>
						<view>
							<!-- 单选题部分 -->
							<radio-group class="block" @change="RadioboxChange" v-if="subject.type===1||subject.type===2">
								<view class="cu-form-group" v-for="(option,index) in subject.optionList" :key="index">
									<radio :value="option.id" :checked="subject.userAnswer.indexOf(option.id) > -1?true:false"></radio>
									<view class="title text-black">{{option.id}}.{{option.content}}</view>
								</view>
							</radio-group>
							<!-- 多选题部分 -->
							<checkbox-group class="block" @change="CheckboxChange" v-else-if="subject.type===3">
								<view class="cu-form-group" v-for="(option,index) in subject.optionList" :key="index">
									<checkbox :value="option.id" :class="subject.userAnswer.indexOf(option.id) > -1?'checked':''" :checked="subject.userAnswer.indexOf(option.id) > -1?true:false"></checkbox>
									<view class="title  text-black">{{option.id}}.{{option.content}}</view>
								</view>
							</checkbox-group>
							<!-- 填空题部分 -->
							<view v-else-if="subject.type===4">
								<view class="cu-form-group solid-bottom">
									<view class="title  text-black">
										答：
									</view>
									<input placeholder="文本输入框" name="input" v-model="subject.userAnswer" @blur="textInput"></input>
								</view>
							</view>
							<!-- 问答题部分,多行文本输入框 -->
							<view v-else-if="subject.type===5">
								<view class="cu-bar cu-bar-title bg-white margin-top">
									<view class="action  text-black">
										答：
									</view>
								</view>
								<view class="cu-form-group solid margin">
									<textarea maxlength="-1" @blur="textInput" v-model="subject.userAnswer" placeholder="多行文本输入框"></textarea>
								</view>
							</view>
						</view>
						<!-- 是否显示正确答案 -->
						<view v-show="subject.showAnswer" class="margin-top solid-top">
							<view class="cu-bar">
								<view class="action  text-grey">
									<text>正确答案：</text>
									<text class="solid-bottom  padding-left text-green">{{subject.answer}}</text>
								</view>
							</view>
							<view class="cu-bar cu-bar-title">
								<view class="action  text-grey">
									<text>解析：</text>
								</view>
							</view>
							<view class="text-content padding  text-grey">
								{{subject.explain}}
							</view>
						</view>
						<view class="submit-exam" v-if="pageIndex == subjectList.length">交卷</view>
					</view>
				</swiper-item>
			</swiper>
		</form>
		<!-- 底部 -->
		<view id="foot-box" class="cu-bar tabbar bg-white shadow foot">
			<view class="action" @click="MoveSubject(-1)">
				<view class="cuIcon-cu-image">
					<text class="lg cuIcon-back text-gray"></text>
				</view>
				<view class="text-gray">上一题</view>
			</view>
			<view class="action" @click="MoveSubject(1)">
				<view class="cuIcon-cu-image">
					<text class="lg text-gray cuIcon-right"></text>
				</view>
				<view class="text-gray">下一题</view>
			</view>

			<!-- <view class="action" @click="FavorSubject">
				<view class="cuIcon-cu-image">
					<text class="lg cuIcon-favor" :class="[userFavor?'text-red':'text-gray']"></text>
				</view>
				<view :class="[userFavor?'text-red':'text-gray']">收藏</view>
			</view> -->

			<!-- <view class="action" @click="ShowAnswerChange">
				<view class="cuIcon-cu-image">
					<text class="lg text-gray cuIcon-question"></text>
				</view>
				<view class="text-gray">{{str}}</view>
			</view> -->
			<!-- <view class="action" @tap="showErrorModal" data-target="modalError">
				<view class="cuIcon-cu-image">
					<text class="lg text-gray cuIcon-warn"></text>
				</view>
				<view class="text-gray">纠错</view>
			</view> -->
		</view>

	</view>
</template>


<script>
	export default {
		data() {
			return {
				h: 0, //定义时，分，秒，毫秒并初始化为0；
				m: 0,
				ms: 0,
				s: 0,
				time: 0,
				str: '',
				pageIndex: 1,
				mytime: '',
				userFavor: false, //是否已收藏
				currentType: 0, //当前题型
				subjectIndex: 0, //跳转索引
				autoShowAnswer: false, //答错是否显答案
				autoRadioNext: true, //判断题、单项题，自动移下一题
				swiperHeight: '800px', //
				title: '2019山东高考原题',
				subjectList: [
					{
						"title": "水是液体？",
						"type": 1,
						"optionList": [{
							"id": "A",
							"content": "对"
						}, {
							"id": "B",
							"content": "错"
						}],
						"answer": "A",
						"userAnswer": "",
						"userFavor": false,
						"explain": "难到是固体不成？"
					},
					{
						"title": "电流分有？",
						"type": 2,
						"optionList": [{
							"id": "A",
							"content": "直流"
						}, {
							"id": "B",
							"content": "交流"
						}, {
							"id": "C",
							"content": "直流和交流"
						}],
						"answer": "C",
						"userAnswer": "",
						"userFavor": false,
						"explain": "科技学依据"
					},
					{
						"title": "酸菜鱼的味道？",
						"type": 3,
						"optionList": [{
							"id": "A",
							"content": "咸味"
						}, {
							"id": "B",
							"content": "辣味"
						}, {
							"id": "C",
							"content": "甜味"
						}, {
							"id": "D",
							"content": "酸味"
						}],
						"answer": "A,B,D",
						"userAnswer": "",
						"userFavor": false,
						"explain": "你怎么想都行，要的就是这个味，答案只能选A,B,D"
					},
					{
						"title": "床前（____）光，疑是地上霜。",
						"type": 4,
						"optionList": [{
							"id": "",
							"content": ""
						}],
						"answer": "明月",
						"userAnswer": "",
						"userFavor": false,
						"explain": "问答题没有选项，无法做答，且不参与计分"
					},
					{
						"title": "什么美国要限制华为？",
						"type": 5,
						"optionList": [{
							"id": "",
							"content": ""
						}],
						"answer": "",
						"userAnswer": "",
						"userFavor": false,
						"explain": "问答题没有选项，无法做答，且不参与计分"
					}
				],
				modalCard: null, //显示答题卡
				modalError: null, //纠错卡
				errorList: ['题目不完整', '答案不正确', '含有错别字', '图片不存在', '解析不完整', '其他错误']
			}
		},
		onReady() {

			var tempHeight = 800;
			var _me = this;
			uni.getSystemInfo({
				//获取手机屏幕高度信息，让swiper的高度和手机屏幕一样高                
				success: function(res) {
					// console.log(res);                    
					tempHeight = res.windowHeight;
					// console.log("屏幕可用高度 " + tempHeight);

					uni.createSelectorQuery().select("#top-box").fields({
						size: true,
						scrollOffset: true
					}, (data) => {
						tempHeight -= data.height;
						// console.log("减掉顶部后的高度 " + tempHeight);

						uni.createSelectorQuery().select("#foot-box").fields({
							size: true,
							scrollOffset: true
						}, (data) => {
							tempHeight -= data.height;
							// console.log("减掉底部后的高度 " + tempHeight);
							_me.swiperHeight = tempHeight + 'px';
							// console.log("滑屏最后高度 " + _me.swiperHeight);
						}).exec();

					}).exec();
				}
			});

		},
		onLoad() {
			// 获取题目类型,默认显示数据的第一种题目的类型
			this.currentType = this.subjectList[0].type;
			//设置头部标题
			uni.setNavigationBarTitle({
				title: this.title
			});

			//添加用户显示答案字段
			for (var i = 0; i < this.subjectList.length; i++) {
				this.$set(this.subjectList[i], "showAnswer", false);
			}
			this.getTime()
		},
		methods: {
			//倒计时方法
			getTime() {
				this.time = setInterval(this.timer, 50)
			},
			timer() { //定义计时函数
				this.ms = this.ms + 50; //毫秒
				if (this.ms >= 1000) {
					this.ms = 0;
					this.s = this.s + 1; //秒
				}
				if (this.s >= 60) {
					this.s = 0;
					this.m = this.m + 1; //分钟
				}
				if (this.m >= 60) {
					this.m = 0;
					this.h = this.h + 1; //小时
				}
				this.str = this.toDub(this.h) + ":" + this.toDub(this.m) + ":" + this.toDub(this.s) + "" /*+this.toDubms(this.ms)+"毫秒"*/ ;
				// document.getElementById('mytime').innerHTML=h+"时"+m+"分"+s+"秒"+ms+"毫秒";
			},
			toDub(n) { //补0操作
				if (n < 10) {
					return "0" + n;
				} else {
					return "" + n;
				}
			},
			//答题板和错题的显示隐藏
			showCardModal: function(e) {
				this.modalCard = e.currentTarget.dataset.target
			},
			hideCardModal: function(e) {
				this.modalCard = null
			},
			showErrorModal: function(e) {
				this.modalError = e.currentTarget.dataset.target
			},
			hideErrorModal: function(e) {
				this.modalError = null
			},
			 //左右滑动事件
			SwiperChange: function(e) {
				//获取当前滑动的索引,默认为0,所以要+1
				console.log(e);
				let index = e.target.current;
				this.pageIndex = index + 1
				if(this.pageIndex == this.subjectList.length){
					uni.showModal({
						cancelText:'取消',
						confirmText:'确定',
						title:'已经是最后一题了',
						success: (res) => {
							if(res.confirm){
								uni.showToast({
									icon:'none',
									title:'赶快交卷吧'
								})
							}
						}
					})
				}
				if (index != undefined) {
					//对当前题型和题目类型重新赋值
					this.subjectIndex = index;
					this.currentType = this.subjectList[index].type;
					this.userFavor = this.subjectList[index].userFavor;
					console.log(this.subjectIndex);
				}
			},
			 //单选选中
			RadioboxChange: function(e) {
				//获取对应题目所有的选项
				var items = this.subjectList[this.subjectIndex].optionList;
				//获取对应value
				var values = e.detail.value;
				this.subjectList[this.subjectIndex].userAnswer = values;
				if (this.autoRadioNext && this.subjectIndex < this.subjectList.length - 1) {
					this.subjectIndex += 1;
				};
				console.log(items,values);
			},
			 //复选选中
			CheckboxChange: function(e) {
				var items = this.subjectList[this.subjectIndex].optionList;
				var values = e.detail.value;
				this.subjectList[this.subjectIndex].userAnswer = "";
				//先循环全部的题目选项
				for (var i = 0, lenI = items.length; i < lenI; ++i) {
					//在循环点击的选项
					for (var j = 0, lenJ = values.length; j < lenJ; ++j) {
						if (items[i].id == values[j]) {
							this.subjectList[this.subjectIndex].userAnswer += items[i].id;
							// console.log(this.subjectList[this.subjectIndex].userAnswer);
							break
						}
					}
				}
			},
			 //填空题
			textInput: function(e) {
				this.subjectList[this.subjectIndex].userAnswer = e.detail.value;
			},
			 //点击显示答案
			ShowAnswerChange: function(e) {
				if (this.subjectList[this.subjectIndex].showAnswer) {
					this.subjectList[this.subjectIndex].showAnswer = false;
				} else {

					this.subjectList[this.subjectIndex].showAnswer = true;
				}
			},
			 //点击收藏题
			FavorSubject: function(e) {
				if (this.userFavor) {
					this.userFavor = false;
					this.subjectList[this.subjectIndex].userFavor = false;
				} else {
					this.userFavor = true;
					this.subjectList[this.subjectIndex].userFavor = true;
				}
			},
			 //上一题、下一题
			MoveSubject: function(e) {
				if (e === -1 && this.subjectIndex != 0) {
					this.subjectIndex -= 1;
				}
				if (e === 1 && this.subjectIndex < this.subjectList.length - 1) {
					this.subjectIndex += 1;
				}
			},
			 //题卡指定,跳转到指定题
			assignSubject: function(e) {
				this.modalCard = null;
				this.subjectIndex = e;
			},
			 //提交纠错
			SubmitError: function(e) {
				this.modalError = null;
			}
		}
	}
</script>

<style>
	@import "../../common/icon.css";
	@import "../../common/main.css";
	@import "../../common/animation.css";
	page {
		background-color: #FFFFFF;
	}

	.cu-form-group {
		justify-content: flex-start
	}

	.cu-form-group .title {
		padding-left: 30upx;
		padding-right: 0upx;
	}

	.cu-form-group+.cu-form-group {
		border-top: none;
	}

	.cu-bar-title {
		min-height: 50upx;
	}
	
	.cu-list.menu>.cu-item-error{justify-content: flex-start;}

</style>
