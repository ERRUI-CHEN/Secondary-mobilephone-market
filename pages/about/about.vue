<template>
	<view class="">
		    <view class="uni-title">
				品牌简介
			</view>
			<view class="uni-text">
				<text>
					手信严选是预见未来网络科技工作室旗下的手机数码销售平台.为用户提供优质二手手机,平板,笔记本,配件等(包含新品)商品的销售及售后服务.
				</text>
		<!-- 		<view class="uni-title"></view>
				<view v-for="(item,index) in probleminfo" :key="item" v-if="index<111" class="uni-mid">
				{{index+1}}.{{item.title}}
				<view class="uni-wenti">{{item.summary}}</view>
				</view> -->
			</view>
			
			<view class="uni-title-one">
				我们承诺
			</view>
			<view class="uni-text">
				<text >
					官方自营,假一赔十,顺丰包邮,7天无理由退货,180天质保.
					\n 手信严选是在经过138道严苛的质检流程后进行包装出库,商品内部有手信严选优品专属防拆标,手机配件等.在手信严选商城,用户可以闭着眼睛放心买,因为每台手机都是死经过各个环节层层把关后的手机精品.
				</text>
			</view>
			
			<view class="uni-title-two">
				物美价廉
			</view>
			<view class="uni-text">
				<text>
					手信严选的供应链直接对接国内领先二手回收商-手信严选回收,以及各大品牌方;纯自营,拒绝翻新,假一赔十,保证用户只为二手原装商品的品质买单.
					\n
					新机的品质,低至5折的价格,无需卖肾,想换就换,支持以旧换"新".
					\n
					有任何疑问,可通过手信严选中的在线客服与我们取得联系.可以拨打客服热线17351015107,服务时间:每日9:00-23:00.
				</text>
					
					
			</view>
	</view>

</template>

<script>
	// import{
	// 	myRequestPost3
	// }from '@/utils/zgrequest.js'
	// export default {
	// 	data() {
	// 		return {
	// 			aboutinfo:{}
	// 		}
	// 	},
	// 	onLoad(options) {
	// 		this.postAbout();
	// 	},
	// 	methods: {
	// 		async postAbout() {
	// 			const res = await myRequestPost3(
	// 				'/sapi/gateway/boss-system-api/nb-agreement/by-type'
	// 			)
	// 			this.aboutinfo =res.data.id
	// 			console.log(this.aboutinfo);
	// 		}
	// 	},
	// }
</script>

<style>
	.uni-title{
		font-weight: 700;
		font-size: 40rpx;  
		line-height: 30px;
	}
 	.uni-text{
		font-size: 35rpx;
		font-weight: 350;
	} 
/* 	.uni-text-one{
		font-size: 35rpx;
		font-weight: 350;
	} */
	.uni-title-one{
		font-weight: 700;
		font-size: 40rpx;  
		line-height: 30px;
		margin-top: 80rpx;
	}
	.uni-title-two{
		font-weight: 700;
		font-size: 40rpx;  
		line-height: 30px;
		margin-top: 80rpx;
	}
</style>
