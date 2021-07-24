<template>
	<view class="goods">
		<swiper indicator-dots :autoplay="true" :interval="2000" indicator-color="#330867" circular indicator-active-color="#30cfd0">
			<swiper-item v-for="item in lunboinfo" :key="item">
				<!--轮播图-->
				<image :src="item"></image>
			</swiper-item>
		</swiper>
		
		<view class="good_info">
			<view class="price">
				<text>￥{{info.sellingPrice}}</text><text @click="open" class="textshare">分享</text>
			</view>
			<view class="goods_title">{{info.shopName}}</view>
		</view>
		<!--这里没有完成，抽屉效果没有，没有实现模块化-->
		<view class="baozhang">
			<view class="chengnuo">
				<view class="zuo">
					<image src="https://gitee.com/SSSSChange/image/raw/master/%E4%BA%8C%E6%89%8B%E6%89%8B%E6%9C%BA/commodity/bao1.png" mode=""></image>
				</view>
				<view class="demo" >{{info.shopName}}</view>
				
				<uni-popup ref="share" background-color="#fff" type="share"><uni-popup-share></uni-popup-share></uni-popup>
			</view>
		</view>
		<!--上面效果没有实现-->
		<view class="hot_goods">
			<view class="tit">热销商品</view>
			<view class="goods_list">
				<view class="goods_item" v-for="(item,index) in goods" :key="item.skuCode" @click="itemClick1(item)">
					<image :src="item.shopMainUrl"></image>
					<view class="tit">
						<text>{{item.prdName}}</text>
						<view class="price1">
							<text>￥{{item.minPrice}}</text>
						</view>
					</view>
				</view>
			</view>
		</view>
		<view class="good_detail">
			<view class="content">
				<image src="https://gitee.com/SSSSChange/image/raw/master/%E4%BA%8C%E6%89%8B%E6%89%8B%E6%9C%BA/commodity/tu1.png" style="width: 750rpx;" mode="widthFix"></image>
			</view>
		</view>
		<view class="hot_wenti">
			<view class="titi" @click="itemClick()">
				<view class="chang">常见问题</view>
				<view class="wen1">更多>></view>
			</view>
			<view class="goods_list">
				<view class="goods_wenti" v-for="(item,index) in wenti" :key="item" v-if="index<3">
					<view class="wen1">
						{{index+1}}.{{item.title}}
					</view>
					<view class="wen">
						{{item.summary}}
					</view>
				</view>
			</view>
		</view>
		<!--购买提交-->
		<view class="goods_nav" v-for="item in goods" :key="item.skuCode">
			<view class="tu" @click="tel"><!--连接到微信-->
				<image class="img" src="https://gitee.com/SSSSChange/image/raw/master/%E4%BA%8C%E6%89%8B%E6%89%8B%E6%9C%BA/commodity/kefu.jpg" style="width: 50rpx;height: 50rpx;"></image>
				<view class="ke" >客服</view>
			</view>
			<text>￥{{info.sellingPrice}}</text>
			<view class="shop" @click="itemClick2(info)">
				<button>立即购买</button>
			</view>
		</view>
	</view>
</template>
<script>
	
	import {
		myRequestGet
	} from '@/utils/zgrequest.js'
	import {
		myRequestPost2
	} from '@/utils/zgrequest.js'
	
	export default {
	
		data() {
			return {
				skuCode: null,
				lunboinfo: [],
				info: {},
				goods: {},
				wenti: {},
				buttonGroup: [
					{
						text: '立即购买',
						backgroundColor: '#ffa200',
						color: '#fff'
					}
				],
				erprdId:"",
				erskuCode:"",
				skuKey:false,
				skuMode:1,
				goodsInfo:{}
			}
		},
		onLoad(options) {
		
			this.erprdId = options.prdId;
			this.erskuCode = options.skuCode;
			console.log("---------");
			console.log(options);
			console.log("---------");
			this.getDetail();
			this.getDetailInfo();
		
			
			
			this.getGoods();
			
			this.getWenti();
		},
		methods: {
			
			
			 open(){
			  
			        this.$refs.share.open()
			      },
			async getDetail() {
				let a=this.erprdId;
				let b=this.erskuCode;
				const res = await myRequestGet(
					`/sapi/gateway/shs-mall-api/v1/goods/goods-detail-v2?shopCode=alipayshop&prdId=${a}&skuCode=${b}&channelId=79595`
				)
				this.lunboinfo = res.data.goods.skuImageList
			},


			async getDetailInfo() {
				let a=this.erprdId;
				let b=this.erskuCode;//分割图片
				const res = await myRequestGet(
					`/sapi/gateway/shs-mall-api/v1/goods/goods-detail-v2?shopCode=alipayshop&prdId=${a}&skuCode=${b}&channelId=79595`
				)
				this.info = res.data.goods
				console.log(this.info);
			},
			//宫格
			async getGoods() {
				const res = await myRequestPost2(
					"/sapi/gateway/shs-mall-api/v1/goods/goods-list/page-info", {
						groupName: "热销机型",
						size: 6,
						skuStatus: 1,
						stockStatusstockStatus: 1
					}
				)
				this.goods = res.data
				console.log(this.goods);
			},

			async getWenti() {
				const res = await myRequestGet(
					"/sapi//gateway/online-sapi/v1/knowledge/mmenu/getNbKnowledge?code=shanfish_mine"
					
				)
				this.wenti = res.data
				console.log(this.wenti);
			},
tel:function(){
				uni.makePhoneCall({
					phoneNumber:"17351015107"
				})
			},
			itemClick1(item) {
				uni.navigateTo({
					url: `/pages/commodity/commodity?prdId=${item.prdId}&skuCode=${item.skuCode}`
				})
			},
			itemClick() {
				uni.navigateTo({
					url: '/pages/problem/problem'
				})
			},
			itemClick2(item) {
				uni.navigateTo({
					url: `/pages/submit/submit?id=${item.prdId}&skuCode=${item.skuCode}`
				}),
				console.log(item.skuCode);
             //支付页面
			}
			
		}
	}
</script>

<style lang="less">
	.goods swiper {
		height: 700rpx;
		background-color: #eee;
		margin: 5px;
	}
	.goods swiper image {
		width: 100%;
		height: 100%;
	}
	.goods_list {
		display: flex;
		padding: 0 15rpx;
		justify-content: space-between;
		overflow: hidden;
		flex-wrap: wrap;
	}
	.goods_item {
		width: 235rpx;
		margin-bottom: 15rpx;
		background: #fff;
		padding: 10px;
		box-sizing: border-box;
	}
	image {
		height: 142rpx;
		width: 100%;
		mix-width: 320rpx;
		margin: 10px auto;
	}
	.good_info {
		padding: 10px;
		background-color: #eee;
		margin: 5px;
		
	}
	.price {
		font-size: 40rpx;
		color: red;
		line-height: 80rpx;
		.textshare{
			color: black;
			font-size: 20rpx;
			margin-left: 500rpx;
		}
	}
	.price1 {
		font-size: 25rpx;
		color: red;
		line-height: 50rpx;
	}
	.goods_title {
		font-size: 32rpx;
		line-height: 60rpx;
	}
	.baozhang {
		margin: 20rpx;
		image{
			height: 175rpx;
			width: 100%;
		}
		.demo {
			 overflow: hidden;
		    white-space: nowrap; // 处理元素内的空白：不换行
		    text-overflow: ellipsis; //文本溢出处理方式：显示省略号
		}
	}
	.good_detail {
		padding-bottom: 50px;
		width: 100%;
		height: 5000rpx;
	}
	.tit {
		text-align: center;
		font-size: 20rpx;
		padding-left: 10px;
		border-bottom: 1px solid #eee;
		line-height: 30rpx;
	}
	.content {
		width: 100%;
	}
	.good-detail image {
		width: 100%;
		height: 100%;
		padding: 10px;
	}
	.hot_wenti {
		margin-top: 3130rpx;
		color: #ccc;
		.wen1 {
			color: black;
		}
		.goods_wenti {
			margin: 10rpx 35rpx;
			width: 700rpx;
		}
		.titi {
			margin: 28rpx;
			display: flex;
			justify-content: space-between;

			.chang {
				font-size: 35rpx;
				color: black;
			}
		}
	}
	.goods_nav {
		position: fixed;
		bottom: 0;
		width: 100%;
		background-color: white;
		display: flex;
		justify-content: space-around;
		.img{
			position: fixed;
			bottom: 45rpx;
		}
		.ke {
			position: fixed;
			bottom: 15rpx;
			font-size: 26rpx;
		}

		text {
			color: red;
			font-size: 50rpx;
			text-align: center;
			line-height: 110rpx;
		}
		button {
			background-color: red;
			color: white;
			height: 90rpx;
			margin-bottom: 30rpx;
			margin-top: 10rpx;
			width: 100%;
			border-radius: 50rpx;
			line-height: 90rpx;
		}
	}
	.payInfo {
		padding: 20rpx 40rpx;
		border-top: 1px solid #e3e3e3;
		display: flex;
		justify-content: flex-end;
	}
	
	.share {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: column;
	}
	.share .button {
		/* #ifndef APP-NVUE */
		width: 100%;
		/* #endif */
		margin: 0;
		margin-top: 10px;
		padding: 3px 0;
		flex: 1;
	}
</style>
