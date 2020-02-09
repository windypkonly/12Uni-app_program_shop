<template>
	<view class="contact">
		<image class="img" src="/static/img/gywmban.jpg"></image>
		<view class="info">
			<view @click="phone">联系电话：136-6501-0621 （点击拨打）</view>
			<view>联系地址：福建省福州市鼓楼区软件园</view>
			<map class="map" 
			     :longitude="longitude" 
				 :latitude="latitude" 
				 :markers="markers"
				 :scale="scale"></map>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				longitude:119.277847,
				latitude:26.115295,
				scale:14,
				markers:[
					{
						longitude:119.277847,
						latitude:26.115295,
						iconPath:'../../static/logo.png',
						width:30,
						height:30
					}
				]
			}
		},
		methods: {
			phone() {
				uni.makePhoneCall({
					phoneNumber: '136-6501-0621'
				})
			}
		}
	}
</script>

<style lang="scss">
	.contact {
		.img {
			width: 750rpx;
			height: 320rpx;
		}
		.info {
			padding: 10rpx 20rpx;
			font-size: 30rpx;
			view {
				line-height: 80rpx;
				border-bottom: 1px dashed #eee;
			}
		}
		.map {
			width: 750rpx;
			height: 750rpx;
		}
	}
</style>
