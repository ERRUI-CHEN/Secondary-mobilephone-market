<template>
	<!-- 搜索框 -->
	<view class="container">
		<view class="head" @click="tosearch">
			<view class="search">
				<text>输入你要购买的机型</text>
			</view>
		</view>
		<!-- 轮播图 -->
		<view class="swipercontainer">
			<swiper class="swiper" :indicator-dots="true" indicator-active-color="#ffffff" @click="topromise">
				<swiper-item>
					<view class="swiper-item uni-bg-red">
						<image :src="swiperlist.bannerurl" mode=""></image>
					</view>
				</swiper-item>
			</swiper>
		</view>
		<!-- 品牌列表 -->
		<view class="mobilelist">
			<uni-grid :column="4" :showBorder="false" :square="false" :highlight="false">
				<uni-grid-item v-for="item in mobileitems" :key="item.name">
					<view @click="tosearchresult(item.name)">
						<image style="width: 80rpx;height:80rpx;" :src="item.icon" mode=""></image>
						<text class="text" style="display: block;font-weight: bold;">{{item.name}}</text>
					</view>
				</uni-grid-item>
			</uni-grid>
		</view>
		<!-- 二手保障 -->
		<view class="adlist" @click="topromise">
			<image style="width: 40rpx;height: 40rpx;margin-top: 20rpx;" :src="require('@/static/index/保障图标.png')" mode=""></image>
			<view>二手保障</view>
			<image :src="require('@/static/index/正品图标.png')" mode=""></image>
			<view>国行正品</view>
			<image :src="require('@/static/index/七天无理由退换图标.png')" mode=""></image>
			<view>7天无理由</view>
			<image :src="require('@/static/index/品质保图标.png')" mode=""></image>
			<view>180天质保</view>
		</view>
		<!-- 每日特价 -->
		<view class="everyday">
			<image :src="require('@/static/index/每日特价背景块.png')"></image>
			<view class="productlist">
				<uni-grid :column="3" class="gard" :highlight="false">
					<uni-grid-item v-for="item in dailyspecial" :key="item.prdId">
						<view @click="tocommodity(item)">
							<image :src="item.shopMainUrl"></image>
							<text class="count">剩余{{item.stockNum}}台</text>
							<text class="mobilename">{{item.prdName}}</text>
							<text class="price">￥{{item.sellingPrice}}</text>
						</view>
					</uni-grid-item>
				</uni-grid>
			</view>

		</view>
		<!-- 二手手机成色标准轮播图 -->
		<view class="swipermobile">
			<swiper class="swiper" :autoplay="true" @click="topromise">
				<swiper-item>
					<view class="swiper-item uni-bg-red">
						<image :src="require('@/static/index/中间广告bnner.png')" mode=""></image>
					</view>
				</swiper-item>
			</swiper>
		</view>
		<!-- 千元神机和爆款好物 -->
		<view class="mobilelistcard">
			<view class="card-left" @click="tosearchresult(item.tip1)" v-for="item in tips" :key="item.id">
				<text class="tip1">{{item.tip1}}</text>
				<text class="tip2">{{item.tip2}}</text>
				<text class="tip3">{{item.tip3}}</text>
				<image v-if="item.image" :src="item.image" mode=""></image>
			</view>
		</view>
		<!-- 商品选项卡 -->
		<view class="productcontent">
			<uni-segmented-control :current="current" :values="items" @clickItem="onClickItem" styleType="text"
				activeColor="red"></uni-segmented-control>
			<view class="content">
				<view v-if="current === 0">
					<uni-grid :column="2" :highlight="false">
						<uni-grid-item v-for="item in gussyoulikelist" :key="item.id">
							<view @click="tocommodity(item)">
								<view class="picture">
									<image :src="item.prdImgUrl" mode=""></image>
								</view>
								<text class="name">{{item.shopName}}</text>
								<text class="price">￥{{item.sellingPrice}}</text>
								<text class="follow">{{item.views}}人关注</text>
							</view>

						</uni-grid-item>

					</uni-grid>
				</view>
				<view v-if="current === 1">
					<uni-grid :column="2" :highlight="false">
						<uni-grid-item v-for="item in mobilelist" :key="item.id">
							<view @click="tocommodity(item)">
							<view class="picture">
								<image :src="item.prdImgUrl" mode=""></image>
							</view>
							<text class="name">{{item.shopName}}</text>
							<text class="price">￥{{item.sellingPrice}}</text>
							<text class="follow">{{item.views}}人关注</text>
							</view>
						</uni-grid-item>
					</uni-grid>
				</view>
				<view v-if="current === 2">
					<uni-grid :column="2" :highlight="false">
						<uni-grid-item v-for="item in padlist" :key="item.id">
							<view @click="tocommodity(item)">
							<view class="picture">
								<image :src="item.prdImgUrl" mode=""></image>
							</view>
							<text class="name">{{item.shopName}}</text>
							<text class="price">￥{{item.sellingPrice}}</text>
							<text class="follow">{{item.views}}人关注</text>
							</view>
						</uni-grid-item>
					</uni-grid>
				</view>
				<view v-if="current === 3">
					<uni-grid :column="2" :highlight="false">
						<uni-grid-item v-for="item in mobileborderlist" :key="item.id">
							<view @click="tocommodity(item)">
							<view class="picture">
								<image :src="item.prdImgUrl" mode=""></image>
							</view>
							<text class="name">{{item.shopName}}</text>
							<text class="price">￥{{item.sellingPrice}}</text>
							<text class="follow">{{item.views}}人关注</text>
							</view>
						</uni-grid-item>
					</uni-grid>
				</view>
			</view>
		</view>
		<uni-load-more v-if="hasmore" :status="'loading'" :showIcon="true" :iconType="'snow'"></uni-load-more>
		<uni-load-more v-else :status="'nomore'" :showIcon="true" :iconType="'snow'"></uni-load-more>
	</view>

</template>

<script>
	import {
		myRequestGet,
		myRequestPost2,
		myRequestPost
	} from '../../utils/zgrequest.js'
	export default {
		data() {
			return {
				flag: true,
				pageSize: 6,
				currentPage: 1,
				totalCount: '',
				swiperlist: [],
				dailyspecial: [],
				gussyoulikelist: [],
				mobilelist: [],
				padlist: [],
				mobileborderlist: [],
				hasmore: true,
				tips:[
					{   
						id:1,
					    tip1:'千元神机',
						tip2:'送家人、游戏机',
						tip3:'立即抢购',
						image:'../../static/index/千元机手机图片.png'
					},
					{   
						id:2,
					    tip1:'爆款好物',
						tip2:'优质低价赶快抢',
						tip3:'立即抢购'
					}
				],
				mobileitems: [{
						name: '苹果',
						icon: '../../static/index/苹果图标.png'
					},
					{
						name: '华为',
						icon: '../../static/index/华为图标.png'
					},
					{
						name: '小米',
						icon: '../../static/index/小米图标.png'
					},
					{
						name: '荣耀',
						icon: '../../static/index/荣耀图标.png'
					},
					{
						name: '三星',
						icon: '../../static/index/三星图标.png'
					},
					{
						name: 'oppo',
						icon: '../../static/index/oppo图标.png'
					},
					{
						name: 'vivo',
						icon: '../../static/index/vivo图标.png'
					},
					{
						name: '平板',
						icon: '../../static/index/平板.png'
					}
				],
				items: ['猜你喜欢', '手机', '平板电脑', '手机周边'],
				current: 0,
			}
		},
		created() {
			this.getswiperpic()
			this.getdailyspecial()
			this.gussyoulike()



		},
		methods: {
			onClickItem(res) {
				this.pageSize = 6
				this.current = res.currentIndex
				// console.log(this.current)
				if (this.current == 0) {
					this.gussyoulike()
				} else if (this.current == 1) {
					this.getmobilelist()
				} else if (this.current == 2) {
					this.getpadlist()
				} else {
					this.getmobileborderlist()
				}

			},
			async getswiperpic() {
				let result = await myRequestGet(
					'/sapi/gateway/shs-mall-api/v1/main-page/cache-info?channelId=79595&modelId=20')
				// console.log(result.data.bsBannerList)
				this.swiperlist = result.data.bsBannerList[0]
			},
			async getdailyspecial() {
				let result = await myRequestPost2("/sapi/gateway/shs-mall-api/v1/goods/goods-list/page-info", {
					groupName: "今日特价",
					size: 3,
					skuStatus:1,
					stockStatus:1
				})
				this.dailyspecial = result.data
				// console.log(this.dailyspecial)
			},
			tosearch() {
				uni.navigateTo({
					url: "../../pages/search/search"
				})
			},
			topromise() {
				uni.navigateTo({
					url: "../../pages/promise/promise"
				})
			},
			tosearchresult(item) {
				uni.navigateTo({
					url: `../../pages/searchresult/searchresult?item=${item}`
				})
			},
			tocommodity(item) {
				uni.navigateTo({
					//详情页面可以通过onload中opition取出来
					url: `../../pages/commodity/commodity?prdId=${item.prdId}&&skuCode=${item.skuCode}`
				})
				
			},
			//猜你喜欢
			async gussyoulike() {
				let index = 0
				let result = await myRequestPost("/sapi/gateway/shs-mall-api/v1/goods/get-good-by-type", {
					"currentPage": 1,
					"pageSize": this.pageSize,
					"prdSaleType": -1,
					"shopCode": "alipayshop"
				})
				this.totalCount = result.data.totalCount
				let likeresult = result.data.list.map(item => {
					item.id = index++
					return item
				})

				this.gussyoulikelist = likeresult
				if (this.pageSize >= this.totalCount) {
					this.hasmore = false
				}
				// console.log(this.pageSize,this.totalCount)

			},
			//手机
			async getmobilelist() {
				let index = 0
				let result = await myRequestPost("/sapi/gateway/shs-mall-api/v1/goods/get-good-by-type", {
					"currentPage": 1,
					"pageSize": this.pageSize,
					"prdSaleType": 1,
					"shopCode": "alipayshop"
				})
				this.totalCount = result.data.totalCount
				let mobileresult = result.data.list.map(item => {
					item.id = index++
					return item
				})

				this.mobilelist = mobileresult
				if (this.pageSize >= this.totalCount) {
					this.hasmore = false
				}
				// console.log(this.pageSize,this.totalCount)
			},
			//平板电脑
			async getpadlist() {
				let index = 0
				let result = await myRequestPost("/sapi/gateway/shs-mall-api/v1/goods/get-good-by-type", {
					"currentPage": 1,
					"pageSize": this.pageSize,
					"prdSaleType": 2,
					"shopCode": "alipayshop"
				})
				this.totalCount = result.data.totalCount

				let padresult = result.data.list.map(item => {
					item.id = index++
					return item
				})
				this.padlist = padresult
				if (this.pageSize >= this.totalCount) {
					this.hasmore = false
				}
				// console.log(this.pageSize,this.totalCount)
			},
			//手机周边
			async getmobileborderlist() {
				let index = 0
				let result = await myRequestPost("/sapi/gateway/shs-mall-api/v1/goods/get-good-by-type", {
					"currentPage": 1,
					"pageSize": this.pageSize,
					"prdSaleType": 0,
					"shopCode": "alipayshop"
				})
				this.totalCount = result.data.totalCount
				let mobileborderresult = result.data.list.map(item => {
					item.id = index++
					return item
				})
				this.mobileborderlist = mobileborderresult
				if (this.pageSize >= this.totalCount) {
					this.hasmore = false
				}
				// console.log(this.pageSize,this.totalCount)
			},
			onReachBottom() {
				this.hasmore = true
				let pageSize = this.pageSize
				pageSize += 6
				this.pageSize = pageSize
				if (this.current == 0) {
					this.gussyoulike()
				} else if (this.current == 1) {
					this.getmobilelist()
				} else if (this.current == 2) {
					this.getpadlist()
				} else {
					this.getmobileborderlist()
				}

			},
			onPullDownRefresh() {
				this.pageSize = 6
				this.gussyoulike()
				setTimeout(function() {
					uni.stopPullDownRefresh();
				}, 500);
			}
		}
	}
</script>

<style lang="less">
	.container {
		background-color: #EBEEF5;
	}

	.head {
		width: 100%;
		height: 80rpx;
		 background-image: linear-gradient(to top, #fff,#330867);
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.search {
		width: 90%;
		height: 70rpx;
		border-radius: 30rpx;
		background-color: #EEEEEE;
		line-height: 70rpx;
		text-align: center;

	}

	.search text {
		color: grey;
	}

	.swipercontainer {
		margin: 10rpx 20rpx;
		image {
			width: 100%;
			height: 300rpx;
			border-radius: 10rpx;
		}
	}

	.mobilelist {
		background-color: white;
		margin: 10rpx 20rpx;
		border-radius: 10rpx;

		uni-grid {
			text-align: center;

		}

		uni-grid-item {
			margin: 20rpx 0;
		}
	}


	.adlist {
		display: flex;
		margin: 0 20rpx;
		width: 95%;
		height: 80rpx;
		line-height: 80rpx;
		background-color: #fdefe2;
		border-radius: 10rpx;
        image{
        	width: 25rpx;
        	height: 25rpx;
			margin-top: 30rpx;
			margin-left: 20rpx;
        }
		view {
			flex: 1;
			font-size: 25rpx;
			text-align: center;
			margin-right: 10rpx;
			color:#946e41;
			
		}

	}

	.everyday {
		width: 95%;
		height: 80rpx;
		margin: 20rpx 20rpx;
		border-radius: 10rpx;

		image {
			width: 100%;
			height: 80rpx;
		}

		.productlist {
			text-align: center;

			uni-grid-item {
				background-color: white;
				border-radius: 10rpx;
			}

			view {

				image {
					width: 50%;
					height: 100rpx;
					margin-top: 10rpx;


				}

				.count {
					display: block;
					background-color: red;
					width: 50%;
					margin-left: 60rpx;
					border-radius: 50rpx;
					color: white;
					font-size: 20rpx;
				}

				.mobilename {
					font-size: 20rpx;
					white-space: nowrap;
				}

				.price {
					margin-top: 10rpx;
					color: red;
					font-size: 25rpx;
					display: block;
				}
			}
		}

	}

	.swipermobile {
		width: 94%;
		height: 120rpx;
		margin-top: 260rpx;
		margin-bottom: 20rpx;
		margin-left: 20rpx;
		border-radius: 10rpx;
        .swiper{
			height: 120rpx;
			image {
				width: 100%;
				height:120rpx;
				border-radius: 10rpx;
			}
		}
		

	}

	.mobilelistcard {
		margin: 10rpx 20rpx;
		display: flex;
		border-radius: 10rpx;


		.card-left {
			height: 150rpx;
			flex: 1;
			position: relative;
			margin-right: 10rpx;
			border-radius: 10rpx;
			background-color: white;

			.tip1 {
				margin-top: 10rpx;
				margin-left: 20rpx;
				display: block;
				font-size: 30rpx;
				font-weight: bolder;
			}

			.tip2 {
				margin-top: 10rpx;
				margin-left: 20rpx;
				display: block;
				font-size: 25rpx;
				color: grey;
			}

			.tip3 {
				margin-top: 10rpx;
				margin-left: 20rpx;
				display: block;
				font-size: 25rpx;
				color: #ff7e00;
			}

			image {
				position: absolute;
				width: 100rpx;
				height: 120rpx;
				left: 230rpx;
				top: 10rpx;
			}
		}

		.card-right {
			height: 150rpx;
			flex: 1;
			border-radius: 10rpx;
			background-color: white;

			.tip1 {
				margin-top: 10rpx;
				margin-left: 20rpx;
				display: block;
				font-size: 30rpx;
				font-weight: bolder;
			}

			.tip2 {
				margin-top: 10rpx;
				margin-left: 20rpx;
				display: block;
				font-size: 25rpx;
				color: grey;
			}

			.tip3 {
				margin-top: 10rpx;
				margin-left: 20rpx;
				display: block;
				font-size: 25rpx;
				color: #ff7e00;
			}
		}
	}

	.content {
		position: relative;

		.picture {
			width: 170rpx;
			height: 170rpx;
			margin-left: 100rpx;
			margin-bottom: 10rpx;

			image {
				margin-top: 40rpx;
				width: 100%;
				height: 100%;

			}
		}

		.name {
			font-size: 25rpx;
			text-align: center;
			margin: 40rpx 10rpx 20rpx;
			overflow: hidden;
			text-overflow: ellipsis;
			display: -webkit-box;
			-webkit-box-orient: vertical;
			-webkit-line-clamp: 2;
		}

		.price {
			font-size: 30rpx;
			margin-left: 30rpx;
			color: red;
		}

		.follow {
			position: absolute;
			bottom: 10rpx;
			right: 20rpx;
			font-size: 20rpx;
			color: grey;
		}

	}

	.productcontent {
		margin: 10rpx 20rpx;

		.content {
			margin-top: 20rpx;
		}

		uni-grid-item {
			background-color: white;
			margin-top: 20rpx;
		}
	}
</style>
