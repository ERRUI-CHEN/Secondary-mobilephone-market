<template>
	<view>
		<!-- 收货地址按钮 -->
		<view class="uni-padding-wrap uni-common-mt">
			<button type="default" @click="goto()" plain class="btn1">编辑收获地址</button>
		</view>
		<!-- 横线 -->
		<view class="">
			<image src="../../static/submit/QQ图片20210514162544.png" mode="" class="img1"></image>
		</view>
		<!-- 商品详情 -->
		<view class="shop">
			<view class="dec">
				<view >
					<image :src="goodsinfo.shopMainUrl" class="commodity"></image>
				</view>
				<view class="shopName">
					{{goodsinfo.shopName}}
				</view>
				<view class="sellingPrice">
					￥{{goodsinfo.sellingPrice}}
				</view>

				<view class="btns">
					<view class="reduce" @click="reduce">
						-
					</view>
					<view class="cart-count">
						1
					</view>
					<view class="add" @click="add">
						+
					</view>
				</view>
			</view>
			<!-- //商品金额 -->
			<view class="price222">
				<text>商品总额</text>
				<view class="sellingPrice2">
					￥{{goodsinfo.sellingPrice}}.00
				</view>
			</view>
			<!-- //商品付款方式 -->
			<view class="pay">
				<label class="payfor">
					<text>选择付款方式</text> <br />
				</label>
				<label class="payy">
					<image src="../../static/submit/微信付款.png" mode="" class="paywx"></image>
					<text style="font-size: 35rpx;line-height: 70rpx;padding-left: 120rpx;">微信付款</text>
					<label class="radio">
						<radio value="" checked="true" color="#F0AD4E" />     <!-- 默认选中微信支付 -->
					</label>
				</label>
			</view>
		</view>
		<!-- 结算按钮 -->
		<view class="bottom">
			<view class="price">
				合计:<text class="sellingPrice3">￥{{goodsinfo.sellingPrice}}.00</text>
			</view>
			<button @click="goto2()" type="warn" class="btn2">结算</button>
		</view>
	</view>
	
</template>

<script>
	import {
		myRequestGet
	} from '@/utils/zgrequest.js'
	export default {
		data() {
			return {
				goodsinfo: {},
				a:""
			}
		},
		onLoad:function(option) {
			this.a=option.skuCode;
			this.getDetail();//顺序不能错
			console.log(this.a);
			console.log("---------");
			console.log(option);
			console.log("---------");
		},
		methods: {
			goto(){
				uni.navigateTo({
					url:"../address/address"
				})
			}, 									//跳转收获地址
			goto2(){
				uni.showToast({
					title: '支付失败',
					duration: 2000,
					icon: 'error',
					mask:'true'
				});
			},	                               //跳转结算
			add() {
				uni.showToast({
					title: '剩余库存不足',
					duration: 2000,
					icon: 'none',
				});
			},
			reduce() {
				uni.showToast({
					title: '数量不得小于0',
					duration: 2000,
					icon: 'none',
				});
			},
			async getDetail() {
				let item=this.a;
				const res = await myRequestGet(
					'/sapi/gateway/shs-mall-api/v1/goods/get-goods-simple-info?skuCode='+item
				)
				this.goodsinfo = res.data
				console.log(this.goodsinfo);
			},
		}
	}
</script>

<style>
	.btn1 {
		width: 300rpx;
		height: 80rpx;
		line-height: 80rpx;
		font-size: 30rpx;
		margin: 20rpx 240rpx;
		border-radius: 50rpx;
	}

	.img1 {
		width: 100%;
		height: 20rpx;
		margin-top: 10rpx;
	}


	/* 商品详情样式 */
	.shop {
		width: 100%;
		height: 1200rpx;
		background-color: #F1F1F1;
		position: relative;
	}

	.dec {
		width: 100%;
		height: 250rpx;
		background-color: #FFFFFF;
		position: relative;
	}

	.commodity {
		width: 250rpx;
		height: 220rpx;
		margin-top: 15rpx;
		margin-left: 20rpx;
		/* background-color: #2C405A ; */
	}

	.shopName {
		position: absolute;
		top: 20rpx;
		left: 270rpx;
		font-size: 35rpx;
	}

	.sellingPrice {
		position: absolute;
		bottom: 20rpx;
		left: 270rpx;
		font-size: 35rpx;
		color: #DD524D;
		font-weight: 800;
	}

	.price222 {
		font-size: 38rpx;
		display: block;
		width: 100%;
		height: 120rpx;
		line-height: 120rpx;
		background-color: #FFFFFF;
		margin-top: 20rpx;
		position: relative;
	}

	.sellingPrice2 {
		font-size: 33rpx;
		font-weight: 400;
		position: absolute;
		right: 60rpx;
		top: 0rpx;
	}

	.cart-count,
	.reduce,
	.add {
		width: 50rpx;
		height: 40rpx;
		text-align: center;
		line-height: 40rpx;
		background-color: #F8F8F8;
		margin: 5rpx;
	}

	.btns {
		display: flex;
		flex-direction: row;
		position: absolute;
		bottom: 20rpx;
		right: 50rpx;
	}


	/* 结算按钮样式 */
	.bottom {
		width: 100%;
		height: 100rpx;
		background-color: #FFFFFF;
		position: fixed;
		bottom: 0rpx;
	}

	.price {
		height: 80rpx;
		line-height: 80rpx;
		margin-left: 240rpx;
	}

	.sellingPrice3 {
		color: #DD524D;
		font-size: 45rpx;
		font-weight: 400;
	}

	.btn2 {
		width: 180rpx;
		height: 80rpx;
		line-height: 80rpx;
		font-size: 30rpx;
		text-align: center;
		border-radius: 50rpx;
		position: absolute;
		top: 10rpx;
		right: 20rpx;
	}

	.pay {
		font-size: 38rpx;
		line-height: 80rpx;
		width: 100%;
		height: 280rpx;
		background-color: #FFFFFF;
		margin-top: 20rpx;
	}

	.payfor {
		display: block;
		width: 100%;
		height: 120rpx;
		line-height: 120rpx;
	}

	.payy {
		width: 100%;
		height: 130rpx;
		line-height: 130rpx;
		position: relative;
	}

	.paywx {
		width: 70rpx;
		height: 70rpx;
		position: absolute;
		left: 20rpx;
		top: 0rpx;
	}

	.radio {
		position: absolute;
		right: -450rpx;
	}

	text {
		padding-left: 30rpx;
	}
</style>
