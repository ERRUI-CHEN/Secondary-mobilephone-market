<template>
	<view class="all">
	<view class="avatar">
<!-- 		<image src="/static/user/cyj.png" @click="changeLogin"></image> -->
	<!-- <button type="default" open-type="getUserInfo" lang="zh_CN"  @getuserinfo="getUserInfo" >登录</button> -->
	<button type="default" v-if="erDefault" @click="erlogin"><image src="../../static/icon/logoblack.png" /></button>
	<view class="eropen">
	<open-data v-if="show" class="avatarUrl" type="userAvatarUrl"></open-data>
    <open-data v-if="show" class="nickName" type="userNickName"></open-data>
	</view>
	</view>
	<view class="mid">
		<uni-grid :column="4" :showBorder="false"  :square="false">
		    <uni-grid-item >
				<image src="/static/user/fukuan.png" mode="" @click="fukuan(1)"></image>
		        <view class="text">待付款</view>
		    </uni-grid-item>
		    <uni-grid-item>
			    <image src="/static/user/fahuo.png" mode="" @click="fukuan(2)"></image>
		        <view class="text">待发货</view>
		    </uni-grid-item>
		    <uni-grid-item>
				<image src="/static/user/shouhuo.png" mode="" @click="fukuan(3)"></image>
		        <view class="text">待收货</view>
		    </uni-grid-item>
		    <uni-grid-item>
				<image src="/static/user/dingdan.png" mode="" @click="fukuan(4)"></image>
		        <view class="text">全部订单</view>
		    </uni-grid-item>
		</uni-grid>
	</view>
		<view class="advertisement">
			<swiper class="swiper" :autoplay="true" @click="shangcheng">
			<swiper-item>
			<view class="swiper-item ">
			<image :src="require('@/static/user/bnner.png')" mode=""></image>
			</view>
			</swiper-item>
			</swiper>
		</view>
		
	<view class="cells">
		<view class="box">
			<image src="/static/user/dizhi.png" mode=""></image>
	        <view class="item" @click="address">管理收货地址</view>
		</view>
		<view class="box">
			<image src="/static/user/kefu.png" mode=""></image>
			<view class="item" @click="tel">在线客服</view>
		</view>
		<view class="box">
			<image src="/static/user/women.png" mode=""></image>
			<view class="item" @click="guanyu">关于我们</view>
		</view>
		<view class="box">
			<image src="/static/user/wenti.png" mode=""></image>
			<view class="item" @click="wenti">常见问题</view>
		</view>
	</view>
		</view>
</template>
<script>
	export default {
		data() {
			return {
				erDefault: true,
				show: false,
				number:""
				
			};
		},
		onLoad(){
			
		},
		methods: {
			fukuan:function(number){
				uni.navigateTo({
					url:`../list/list?active=${number}`
				})
			},
			shangcheng:function(){
				uni.navigateTo({
					url:'../promise/promise'
				})
			},
			wenti:function(){
				uni.navigateTo({
					url:'../problem/problem'
				})
			},
			guanyu:function(){
				uni.navigateTo({
					url:'../about/about'
				})
			},
			address:function(){
				uni.navigateTo({
					url:'../address/address'
				})
			},
			tel:function(){
				uni.makePhoneCall({
					phoneNumber:"17351015107"
				})
			},
				erlogin() {
					let code = '';
					wx.login({
					  success: res=>{
						  code = res.code;
						  		console.log(code);
						  		console.log("登录");
						  		},
						  });
				uni.getUserProfile({
					desc:'登录',
				    success: res => {
						console.log(res);
						console.log('成功了');
						console.log(res.userInfo.avatarUrl);
						console.log(res.userInfo.nickName);
						this.show=true;
						this.erDefault=false;
						},
					fail: res => {
					console.log('失败了');
					uni.showModal({
						title: '提示',
						content: '请先登录！',
						showCancel: true,
						success: function(res) {
							if (res.confirm) {
								console.log('点击确定');
							}else if (res.cancel) {
								console.log('点击取消');		
						}
					}
			});
		}
	});
}
}																					
			
		}
</script>

<style>
	.all{
		width: 100%;
		height: 100%;
	}
	.avatar {
	  display: flex;
	  justify-content: center;
	  align-items: center;
	  height: 350rpx;
	  background-image: linear-gradient(to top, #fff,#330867);
	}
/* 	.avatar image {
	  width: 150rpx;
	  height: 150rpx;
	  border-radius: 50%;
	  box-shadow: 0 0 0 5rpx white;
	} */
	.avatar button{
		 width: 150rpx;
		 height: 150rpx;
		 display: block;
		 border-radius: 50%;
		 background-image: linear-gradient(to top, #330867,#30cfd0);
		 
	}
	.avatar image{
		height: 180rpx;
		width: 180rpx;
		margin-left: -44rpx;
		margin-top: -17rpx;
		
	}
	.avatar .eropen{
		display: flex;
		justify-content: center;
		flex-direction: column;
	}
	.avatar .avatarUrl {
		 width: 150rpx;
		 height: 150rpx;
		 display: block;
		 border-radius: 50%;
		 overflow: hidden;
	}
	.avatar .nickName{
		font-weight: bold;
		margin:auto ;
		margin-top: 20rpx;
	}
	.mid{
		width: 680rpx;
		height: 200rpx;
		background-color: white;
		margin-left: 32rpx;
		border-radius: 5rpx;
	}
	.uni-grid-item{
		text-align: center;
	}
	.uni-grid-item image{
		line-height: 120rpx;
		width: 60rpx;
		height: 60rpx;
		margin: 10px auto;
		font-size: 20px;
		margin-top: 40rpx;
	}
	.advertisement{
		width: 94%;
		height: 120rpx;
		margin-bottom: 20rpx;
		margin-left: 20rpx;
		border-radius: 10rpx;
			}
	.swiper{
		height: 120rpx;
		}
	.swiper image {
		width: 100%;
		height:120rpx;
		border-radius: 10rpx;
		}
	.cells {
	  margin-top: 20rpx;
	}
	.box{
		margin-top: 40rpx;
		display: flex;
		flex-direction: row;
		width: auto;
		height: 80rpx;
		border-bottom: 1rpx solid #eaeaea;
	}
	.box image{
		width: 35rpx;
		height: 35rpx;
		margin-left: 30rpx;
	}
	.item{
		font-size: 30rpx;
		margin-left: 20rpx;
	}
</style>
