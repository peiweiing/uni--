<template>
	<view>
		<view class="anniu" :class="ison!=i? 'onleft':'onright'" v-for="(v,i) in array" @click="discountHandle(v, i)">
		  <!-- <view class="annius"></view> -->
		  <input class="annius" type="radio" v-model="v.text"/>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				ison:'',dikou:'',array:[
					{title:'',text:'点一击'},
					{title:'',text:'点二击'},
					{title:'',text:'点三击'},
				]
			}
		},
		methods: {
			discountHandle(item, vi){
				console.log(item.text);
				let s =vi+1;
				if(s){this.ison=vi;}
			      // this.dikou = value.amount;
			      // this.vamount_items[0].amount = item.order_goods_price;
			      // this.vamount_items[1].amount = item.dispatch_price;
			      // if(this.vamount_items[2].amount){
			      //   this.vamount_items[2].amount = value.amount;
			      // }else{
			      //   this.dikou=0;
			      // }
			},
		}
	}
</script>

<style>

		.anniu{
			display:flex;align-items: center;
			width: 50px;height: 30px;padding: 1px;
			border-radius: 50px; transition: all 0.6s;
		}
		.anniu .annius{
			width: 50%;height: 90%;border-radius: 50%;
			background-color: rgb(255, 255, 255);
			color:transparent;
			text-shadow:0 0 0 red;
			font-size: 0;
		}
		.onleft{
			display: flex;justify-content: flex-start;
			background-color: rgb(223, 223, 223);
		}
		.onright{
			display: flex;justify-content: flex-end;
			background-color: rgb(0, 122, 255);
		}
</style>
