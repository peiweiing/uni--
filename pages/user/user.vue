<template>
	<view>
		<view class="anniu" :class="ison!=i? 'onleft':'onright'" v-for="(v,i) in array" @click="discountHandle(v, i)">
			<!-- <view class="annius"></view> -->
			<!-- <input class="annius" type="radio" v-model="v.text" /> -->
			<input class="annius" type="checked" v-model="v.text" />
		</view>
		123
		<!-- <view v-for="(option, index) in options">
			<view>{{option.name}}</view>
			<text class="span" :class="{select:sel[index] == ind}" v-for="(item, ind) in option.items" @click="select(index, ind)">{{item.msg}}</text>
		</view> -->
		456
		<view class="sortItem" v-for="(item,index) in attrAndValuees" :key="item.attrId">
		    <text>{{item.attrName}}:</text>
		    <view>
				<text v-for="(itemm,ind) in item.valuees" :key="itemm.attrId" :class="{'cur':sel[index] == ind}" @click="selectes(index,ind)" class="hand" >{{itemm.value}}</text>
		    </view>
		</view>
		789
		<view class="chose-ck" v-for="(item,index2) in colors" :key="index2">
			<view class="p">{{item.name}}</view>
			<text class="dt" v-for="(item2,index) in item.childsCurGoods" :key="index" 
				:class="{'check':index === iac[index2]}" @click="chek(index2,index)">
				{{item2.name}}
			</text>
		</view>
		000
	</view>
</template>

<script>
	export default {
		data() {
			return {
				ison: '',
				dikou: '',
				array: [
					{
						title: '',
						text: '点一击'
					},
					{
						title: '',
						text: '点二击'
					},
					{
						title: '',
						text: '点三击'
					},
				],
				
				id: [],
				options: [
					 {
						 items: [
							 {'msg': '绿色',"id": "11",},
							 {'msg':"红色","id": "12"},
						 ],
						 name: "颜色"
					},
					{
						items: [
							{'msg': "XXX","id": "13"},
							{'msg': "L","id": "14"},
							{'msg': "XXL","id": "15"},
						],
						name: "型号"
					},
					{
						items: [
							{'msg': "32G","id": "16"},
							{'msg': "8G","id": "17"},
							{'msg': "4G","id": "18"},
						],
						name: "版本",
					},
				],
				
				sel: [],
				attrAndValuees: [
				    {'attrId': 1,'attrName': '味道',
				        'valuees': [
				            {'attrId': 1,'value': '橘子味'},
				            {'attrId': 2,'value': '草莓味'}
				        ]
				    },
				    {'attrId': 2,'attrName': '容量',
				        'valuees': [
				            {'attrId': 4,'value': '100ml'},
				            {'attrId': 6,'value': '300ml'}
				        ]
				    },
				],
				iac:[0,0],
				"colors": [
					{
						"childsCurGoods": [
								{"dateAdd": "2018-03-05 16:07:58","id": 6819,"name": "16GB","paixu": 0,"propertyId": 2977,"remark": "","userId": 4684},
								{"dateAdd": "2018-03-05 16:08:03","id": 6820,"name": "64GB","paixu": 0,"propertyId": 2977,"remark": "","userId": 4684},
								{"dateAdd": "2018-03-05 16:08:10","id": 6821,"name": "128GB","paixu": 0,"propertyId": 2977,"remark": "","userId": 4684},
								{"dateAdd": "2018-03-05 16:08:16","id": 6822,"name": "256GB","paixu": 0,"propertyId": 2977,"remark": "","userId": 4684}
				        ],
				        "dateAdd": "2018-03-05 16:07:48","id": 2977,"name": "版本","paixu": 0,"userId": 4684
				    },
					{
				        "childsCurGoods": [
				            {"dateAdd": "2018-03-05 16:08:49","id": 6823,"name": "土豪金","paixu": 0,"propertyId": 2978,"remark": "","userId": 4684},
							{"dateAdd": "2018-03-05 16:08:59","id": 6824,"name": "亮银","paixu": 0,"propertyId": 2978,"remark": "","userId": 4684},
							{"dateAdd": "2018-03-05 16:09:05","id": 6825,"name": "亮黑","paixu": 0,"propertyId": 2978,"remark": "","userId": 4684},
							{"dateAdd": "2018-03-05 16:09:10","id": 6826,"name": "亮白","paixu": 0,"propertyId": 2978,"remark": "","userId": 4684}
				        ],
				        "dateAdd": "2018-03-05 16:08:23","dateUpdate": "2018-03-05 16:08:41","id": 2978,"name": "颜色","paixu": 0,"userId": 4684,
					}
				],
			}
		},
		methods: {
			discountHandle(item, vi) {
				console.log(item.text);
				let s = vi + 1;
				if (s) {
					this.ison = vi;
				}
				// this.dikou = value.amount;
				// this.vamount_items[0].amount = item.order_goods_price;
				// this.vamount_items[1].amount = item.dispatch_price;
				// if(this.vamount_items[2].amount){
				//   this.vamount_items[2].amount = value.amount;
				// }else{
				//   this.dikou=0;
				// }
			},
			select: function(index, ind) {
				this.sel[index] = ind; //让数组sel的第index+1的元素的值等于ind
				this.sel = this.sel.concat([]); //因为数组是引用类型，对其中一个变量直接赋值不会影响到另一个变量（并未操作引用的对象），使用concat（操作了应用对象）
				this.id[index] = this.options[index].items[ind].id; //获取选中的id
				this.id = this.id.concat([]);
				console.log(this.id);
			},
			selectes: function (index, ind) {
			      this.sel[index] = ind; 
			      // this.$set(this.sel, index, ind)
			      this.sel = this.sel.concat([]); 
			},
			chek(index2,index){
				this.iac[index2]=index
				this.iac = this.iac.concat([])
			}
		}
	}
</script>

<style>
	/* .select{
		color: red;
		background-color: #0062CC;
	} */
		.hand{
			color: #0062CC;
		}
		.cur{
			background-color: red;
		}
		.span {
	        display: inline-block;
	        padding: 10px 20px;
	        background-color: #666;
	        margin-left: 20px;
	        color: #fff;
	        border-radius: 10px;
	    }
	
	    .select {
	        background-color: aqua;
	    }
	
	    .row {
	        display: inline-block;
	    }
		.chose-ck {
		
		    overflow: hidden;
		}
		
		.chose-ck .dt {
		    padding: .15rem .3rem;
		    border: 1px solid rgba(0, 0, 0, .15);
		    float: left;
		    margin: 0 .2rem .2rem 0;
		    font-size: .28rem;
		    -webkit-transition: all .5s;
		    -moz-transition: all .5s;
		    transition: all .5s;
		}
		
		.chose-ck .dt.check {
		    border: 1px solid #ff6700;
		    color: #ff6700;
		}
		
		.chose-ck .p {
		    color: rgba(0, 0, 0, .87);
		    line-height: .8rem;
		}

	.anniu {
		display: flex;
		align-items: center;
		width: 50px;
		height: 30px;
		padding: 1px;
		border-radius: 50px;
		transition: all 0.6s;
	}

	.anniu .annius {
		width: 50%;
		height: 90%;
		border-radius: 50%;
		background-color: rgb(255, 255, 255);
		color: transparent;
		text-shadow: 0 0 0 red;
		font-size: 0;
	}

	.onleft {
		display: flex;
		justify-content: flex-start;
		background-color: rgb(223, 223, 223);
	}

	.onright {
		display: flex;
		justify-content: flex-end;
		background-color: rgb(0, 122, 255);
	}
</style>
