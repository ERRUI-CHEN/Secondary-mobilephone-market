<template>
	<view>
		<view class="uni-title">
			常见问题
			</view>
	<view v-for="(item,index) in probleminfo" :key="item" v-if="index<10" class="uni-mid">
	{{index+1}}.{{item.title}}
	<view class="uni-wenti">{{item.summary}}</view>
	</view>
	</view>
</template>

<script>
	import {
			myRequestGet2
		} from '@/utils/zgrequest.js'
	export default {
		data() {
			return {
				
				probleminfo:{}
			}
		},
		onLoad(options) {
			 
			this.getProblem();
			
			
		},
		// computed: {
		//     eventProblem: function () {
		//         return this.probleminfo.filter(item=>{
		// 			if(data.length=10){
		// 				return item;
		// 			}
		//      });
		//  },
		methods: {
			async getProblem() {
				const res = await myRequestGet2(
					'/sapi//gateway/online-sapi/v1/knowledge/mmenu/getNbKnowledge?code=shanfish_mine'
				)
				this.probleminfo =res.data
				console.log(this.probleminfo);
			}
		},
		
		}
</script>

<style>
	.uni-title{
		font-weight: 700;  
		font-size: 40rpx;  
		line-height: 30px;
	}
	.uni-mid{
		margin-top: 25rpx;
		font-size: 30rpx;
		font-weight: 300;
	}
	.uni-wenti{
		color: #C0C0C0;
		font-size: 30rpx;
	}
</style>

