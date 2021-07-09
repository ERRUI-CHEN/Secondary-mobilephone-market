<template>
	<view>
		<view class="search" :style="{ backgroundColor: backgroundColor }">
			<view class="content" :style="{ 'border-radius': radius + 'px', border: border }">
				<view class="content-box" :class="{ center: mode === 2 }">
					<text class="icon icon-search">&#xe61c;</text>
					<input class="input" :class="{ center: !active && mode === 2 }" :focus="isFocus"
						:placeholder="placeholder" v-model="inputVal" @focus="focus" @blur="blur" />
					<text v-if="isDelShow" class="icon icon-del" @click="clear">&#xe644;</text>
				</view>
				<view v-show="(active && show && button === 'inside') || (isDelShow && button === 'inside')"
					class="searchBtn" @click="search">搜索</view>
			</view>
			<view class="search-choose">

				<button @click="showDrawer" type="default">筛选</button><!-- 筛选弹窗 -->
				<uni-drawer ref="showRight" mode="right" :mask-click="false">
					<scroll-view>
						<view v-for="item in 1" :key="item.brandId">
							<uni-group title="分类">
								<view class="choose">全部</view>
							</uni-group>
							<uni-group title="品牌">
								<view class="choose">全部</view>
								<view class="choose1" v-for="item in brandList" :key="item.brandId">
									{{item.brandName}}
								</view>
							</uni-group>

							<uni-group title=" ">
								<view style=”white-space:pre-wrap”>
									<view class="choose"> </view>
									<view class="choose4"></view>
								</view>
							</uni-group>


							<uni-group title="价格区间(元)">
								<view>
									<view class="price1">
										0-2999
									</view>
									<view class="price1">
										3000-5999
									</view>
									<view class="price1">
										6000-8999
									</view>
								</view>
							</uni-group>
						</view>

						<view class="search-an">
							<button @click="closeDrawer" type="default">关闭</button>
							<button type="reset" @click="open">重置</button>
							<uni-popup ref="popup" type="center">此功能未开通，整体功能为齐全</uni-popup>
							<button type="submit" @click="open">确定</button>
							<uni-popup ref="popup" type="center">此功能未开通，整体功能为齐全</uni-popup>
						</view>

					</scroll-view>
				</uni-drawer>

			</view>
		</view>
		<view class="all-list">
			<view class="listcontent" v-for="item in goodlist" :key="item.id" @click="tocommodity(item)">
				<image :src="item.prdImgUrl" mode=""></image>
				<view class="listright">
					<view class="name">
						{{item.shopName}}
					</view>
					<view class="price">
						￥{{item.sellingPrice}}
					</view>
				</view>

			</view>


		</view>
		<uni-load-more v-if="hasmore" :status="'loading'" :showIcon="true" :iconType="'snow'"></uni-load-more>
		<uni-load-more v-else :status="'nomore'" :showIcon="true" :iconType="'snow'"></uni-load-more>



	</view>
</template>

<script>
	import {
		myRequestPost,
		myRequestGet
	} from "../../utils/zgrequest.js"
	export default {
		props: {
			mode: {
				type: Number,
				default: 1
			},
			button: {
				type: String,
				default: 'outside'
			},
			show: {
				type: Boolean,
				default: true
			},
			radius: {
				type: String,
				default: '60'
			},
			placeholder: {
				type: String,
				default: '搜索你需要浏览的宝贝'
			},
			backgroundColor: {
				type: String,
				default: '#fff'
			},
			border: {
				type: String,
				default: '1px #f5f5f5 solid'
			}

		},
		data() {
			return {
				active: false,
				inputVal: '',
				searchName: '取消',
				isDelShow: false,
				isFocus: false,
				brandList: [],
				goodlist:[],
				pageSize:10,
				currentPage:1,
				prdSaleType:1,
				brandOrPrd:'',
				hasmore: true,
				goodlistlength:''
				
			};
		},
		onLoad(e) {
			console.log(e.item);
			console.log("-----------")
			if(e.item!="平板"){
				this.brandOrPrd=e.item
			}
			else{
				this.brandOrPrd=''
				this.prdSaleType=2
			}
			
			this.getbrandlist()
			this.getgoodlist()
			if(this.goodlist.length<10){
				this.hasmore=false
			}
			
		},
		
		onReachBottom() {
			console.log(111)
			this.currentPage+=1
			this.getgoodlist()
			
			
			
		},
		methods: {
			focus() {
				this.active = true;
			},
			blur() {
				this.isFocus = false;
				if (!this.inputVal) {
					this.active = false;
				}
			},
			clear() {
				this.inputVal = '';
				this.active = false;
				this.$emit('search', '');
			},
			getFocus() {
				this.isFocus = true;
			},
			search() {
				if (!this.inputVal) return;
				console.log(this.inputVal); //
				this.$emit('search', this.inputVal);
			},
			open() {

				this.$refs.popup.open('center')
			},
			showDrawer() {
				this.$refs.showRight.open();
			},
			closeDrawer() {
				this.$refs.showRight.close();
			},
			tocommodity(item) {
				uni.navigateTo({
					url: `../../pages/commodity/commodity?prdId=${item.prdId}&skuCode=${item.skuCode}`
				})
				console.log(item.prdId)
				console.log(item.skuCode)
			},
			async getbrandlist() {
				let result = await myRequestGet(
					'/sapi/gateway/shs-mall-api/v1/brand/find-brand-data?prdSaleType=1&shopCode=alipayshop')
				// console.log(result)
				this.brandList = result.data.brandList
			},
			async getgoodlist() {
				
				this.hasmore=true
				let result = await myRequestPost('/sapi/gateway/shs-mall-api/v1/goods/get-goods-info-v2',{
						"brandOrPrd":this.brandOrPrd,
						"prdSaleType":this.prdSaleType,
						"prdName": "",
						"startPrice": "",
						"endPrice": "",
						"channelId": 79595,
						"currentPage": this.currentPage,
						"pageSize":this.pageSize
			     })
				  // console.log(result.data.goodsList.length)
				  
				  this.goodlistlength=result.data.goodsList.length
				  let index=0
				  let goodlist=result.data.goodsList
				  if(this.goodlistlength==0){
				  	this.hasmore=false
				  	
				  }
				 
				  this.goodlist=[...this.goodlist,...goodlist]
				 this.goodlist.map(item=>{
				  					  item.id=index++
				  					  return item
				  })
			}


		}

	};
</script>

<style lang="scss" scoped>
	.search {
		display: flex;
		width: 100%;
		border-bottom: 1px #f5f5f5 solid;
		// box-sizing: border-box;
		padding: 15upx;
		// font-size: $uni-font-size-base;
		background: #fff;

		.content {
			// display: flex;
			align-items: center;
			width: 560rpx;
			height: 60rpx;
			border: 1px #ccc solid;
			background: #fff;
			overflow: hidden;
			transition: all 0.2s linear;
			border-radius: 30px;

			.content-box {
				width: 560rpx;
				display: flex;
				align-items: center;
				background-color: #F4F4F4;

				&.center {
					justify-content: center;
				}

				.icon {
					padding: 0 15upx;

					&.icon-del {
						font-size: 38upx;

					}
				}

				.input {
					width: 400rpx;

					line-height: 60upx;
					height: 60upx;
					color: #333;
					font-size: 28upx;

					// transition: all 0.2s linear;
					&.center {
						width: 200upx;
					}

					&.sub {
						// position: absolute;
						width: auto;
						color: grey;
					}
				}
			}
		}
	}

	@font-face {
		font-family: 'iconfont';
		src: url('https://at.alicdn.com/t/font_989023_efq0mtli526.ttf') format('truetype');
	}

	.icon {
		font-family: iconfont;
		font-size: 32rpx;
		// font-style: normal;
		color: #999;
	}

	.search-choose {
		margin-left: 10rpx;
		width: 140rpx;
		height: 80rpx;

		button {
			font-size: 14px;
			width: 120rpx;
			height: 60rpx;
			line-height: 60rpx;


		}

		.search-an button {
			float: left;
			margin-left: 20rpx;
			margin-top: 20rpx;
		}

		.search-an uni-popup {
			color: white;
		}

		.choose,
		.choose1 {
			width: 160rpx;
			height: 46rpx;
			line-height: 46rpx;
			border: 1px soild grayscale($color: #000000);
			background-color: #EBEEF5;
			font-size: 12px;
			border-radius: 50px;
			text-align: center;
			margin-top: 14rpx;
			margin-bottom: -10rpx;

		}

		.choose1,
		.choose3 {
			float: left;
		}




		.price1,
		.price2,
		.price3 {

			width: 120rpx;
			height: 46rpx;
			line-height: 46rpx;
			border: 1px soild grayscale($color: #000000);
			background-color: #EBEEF5;
			font-size: 10px;
			border-radius: 50px;
			text-align: center;
			margin-left: 6rpx;
			margin-top: 16rpx;
			margin-bottom: -10rpx;
			left: -10rpx;
		}

		uni-group view .price1 {
			float: left;
		}






	}

	.all-list {
		width: 95%;
		margin-top: 6rpx;
		
		
		

		.listcontent {
			width: 100%;
			height: 190rpx;
			margin-bottom: 20rpx;
			background-color: #F8F8F8;

			image {
				width: 180rpx;
				height: 190rpx;
				float: left;
			}

			.listright {
				width: 530rpx;
				height: 190rpx;
				margin-left: 180rpx;
				position:relative;
				

				.name {
					margin-left: 40rpx;
                    font-size: 25rpx;
					position:absolute;
					top: 40rpx;

				}

				.price {
					margin-left: 40rpx;
					font-size: 30rpx;
					color: red;
					position:absolute;
					bottom: 20rpx;
				}
			}




		}

	}
</style>
