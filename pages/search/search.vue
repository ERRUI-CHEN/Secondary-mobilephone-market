<template>
	<view>
		<view class="search" >
			<view class="content" :style="{ 'border-radius': radius + 'px', border: border }">
				<view class="content-box" :class="{ center: mode === 2 }">
					<text class="icon icon-search">&#xe61c;</text>
					<input class="input"  :focus="isFocus"
						:placeholder="placeholder" v-model="inputVal" @focus="focus" @blur="blur" />
					<text v-if="isDelShow" class="icon icon-del" @click="clear">&#xe644;</text>
				</view>
				
			</view> 
			<view v-if="button === 'outside'" class="button" :class="{ active: show || active }" @click="search">
				<view class="button-item" @click="tosearchresult">{{ !show ? searchName : '搜索' }}</view>
			</view>
		</view>
		<view class="search-op">大家都搜索</view>
		<view class="search-all">
			
			<view class="search-ju" v-for="item in searchlist" :key="item.prdId">
				<view @click="tocommodity(item)" class="search-it" >
					{{item.prdName}}
				</view>

			</view>
		</view>

	</view>
</template>

<script>
	import {myRequestPost} from"../../utils/zgrequest.js"
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
				// active: false,
				inputVal: '',
				searchName: '取消',
				isDelShow: false,
				isFocus: false,
				swiperlist: [],
				searchlist: [],

			};
		},
		created() {
			this.getsearchlist()
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

			async getsearchlist() {
				let result = await myRequestPost("/sapi/gateway/shs-mall-api/v1/log-buried-point/find-user-browse-info")
				
				this.searchlist=result.data
				// console.log(this.searchlist)
				
			},
			tosearchresult() {
				uni.navigateTo({
					url: "../../pages/searchresult/searchresult"
				})
			},
			tocommodity(item) {
				uni.navigateTo({
					url: `../../pages/commodity/commodity?prdId=${item.prdId}&skuCode=${item.skuCode}`
				})
				console.log(item.prdId)
				console.log(item.skuCode)
			},
		},
		watch: {
			inputVal(newVal) {
				if (newVal) {
					this.searchName = '搜索';
					this.isDelShow = true;
				} else {
					this.searchName = '取消';
					this.isDelShow = false;
				}
			}
		}

	};
</script>


<style lang="scss" >
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
			width: 100%;
			height: 60upx;
			border: 1px #ccc solid;
			background: #fff;
			overflow: hidden;
			transition: all 0.2s linear;
			border-radius: 30px;

			.content-box {
				width: 100%;
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
					width: 100%;
					max-width: 100%;
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

		.button {
			// display: flex;
			align-items: center;
			// justify-content: center;
			// position: relative;
			// flex-shrink: 0;
			width: 60rpx;
			height: 60rpx;
			line-height: 60rpx;
			transition: all 0.2s linear;
			// white-space: nowrap;
			overflow: hidden;

			&.active {
				padding-left: 15upx;
				width: 100upx;
				color: #30cfd0;
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
	.search-op {
		width: 200rpx;
		height: 50rpx;
		margin-top: 20rpx;
		margin-left: 30rpx;
		font-size: 18px;
		font-family: "黑体";
		
		
	}

	.search-all {
		width: 300rpx;
		height: 100%;
		margin-top: 20px;
		margin-left: 20rpx;
		// display: flex;
		margin: auto ;
        // float: right;
		

		.search-ju {
			 width: 300rpx;
			height: 60rpx;
			// display: flex;
			// float: left;
			
			.search-it{
				border: 1px soild grayscale($color: #000000);
				background-color: #EBEEF5;
				width: 300rpx;
				height: 46rpx;
				line-height: 46rpx;
				text-align: center;
				border-radius: 50px;
				font-size: 12px;
				// float: left;
				margin-left: 10rpx;
				// flex-direction:column;
				// flex-wrap:warp;
				// float: left;
				
			}


		}
	}
</style>