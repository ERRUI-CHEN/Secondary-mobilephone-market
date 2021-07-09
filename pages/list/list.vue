<template>
	<view class="warehousingToBeCon">
		<!-- nav -->
		<view class="nav">
			<view class="flex_between">
				<view class="nav_title"><view :class="{ active: isActive == 1 }" @click="chenked(1)">全部</view></view>
				<view class="nav_title"><view :class="{ active: isActive == 2 }" @click="chenked(2)">待付款</view></view>
				<view class="nav_title"><view :class="{ active: isActive == 3 }" @click="chenked(3)">待发货</view></view>
				<view class="nav_title"><view :class="{ active: isActive == 4 }" @click="chenked(4)">待签收</view></view>
			</view>
		</view>
		<!-- nav-item -->
		<view class="nav_item" v-if="isActive == 1"><image src="../../static/user/暂无数据.png" mode="" class="nav_img"></image></view>
		<view class="nav_item" v-if="isActive == 2"><image src="../../static/user/暂无数据.png" mode="" class="nav_img"></image></view>
		<view class="nav_item" v-if="isActive == 3"><image src="../../static/user/暂无数据.png" mode="" class="nav_img"></image></view>
		<view class="nav_item" v-if="isActive == 4"><image src="../../static/user/暂无数据.png" mode="" class="nav_img"></image></view>
		<uni-load-more v-if="erMore" :status="'loading'" :showIcon="true" :iconType="'snow'"></uni-load-more>
	</view>
</template>

<script>
export default {
	data() {
		return {
			isActive: 0,
			erMore: "",
			
			timer: null
		};
	},
	onLoad: function(options) {
		console.log("------"+options.active);
		this.isActive=options.active;
		
		this.open();
		this.chenked();
		
	},

	methods: {
		open(){
			var that=this;
			
			let isActive=this.isActive;
			that.setData({
				isActive
			});
		},
		timeUp() {
			clearInterval(this.timer);
			console.log('定时器执行');
		},
		chenked(type) {
			this.isActive = type;
			this.erMore = true;
			let _this = this;
			this.timer = setInterval(() => {
				_this.erMores();
				this.timeUp();
			}, 2000);

			console.log('这是第' + type + '页面');
		},

		erMores() {
			this.erMore = false;
		}
	}
};
</script>

<style lang="scss" scoped>
.warehousingToBeCon {
	width: 100%;
	background-color: #f2f2f2;

	.nav {
		border-top: 1rpx solid #f2f2f2;
		background-color: #fff;

		.flex_between {
			display: flex;

			.nav_title {
				height: 88rpx;
				line-height: 88rpx;
				width: 100%;
				text-align: center;
				font-size: 32rpx;
				font-family: 'PingFang';
				color: rgb(102, 102, 102);
			}
		}
	}
}

.active {
	position: relative;
	color: #31d378;
}

.active::after {
	content: '';
	position: absolute;
	width: 100rpx;
	height: 4rpx;
	background-color: #31d378;
	left: 0px;
	right: 0px;
	bottom: 0px;
	margin: auto;
}

.nav_item {
	position: relative;
}

.nav_img {
	position: absolute;
	width: 400rpx;
	height: 350rpx;
	top: 180rpx;
	left: 25%;
}
</style>
