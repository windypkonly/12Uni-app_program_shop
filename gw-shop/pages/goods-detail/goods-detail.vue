<template>
	<view class="goods_detail">
		<swiper indicator-dots>
			<swiper-item v-for="item in swipers" :key="item.src">
				<image :src="item.src"></image>
			</swiper-item>
		</swiper>
		
		<view class="box1">
			<view class="price">
				<text>￥{{info.sell_price}}</text>
				<text>￥{{info.market_price}}</text>
			</view>
			<view class="goods_name">{{info.title}}</view>
		</view>
		
		<view class="line"></view>
		
		<view class="box2">
			<view>货号：{{info.goods_no}}</view>
			<view>库存：{{info.stock_quantity}}</view>
		
		<view class="line"></view>
		
		<view class="box3">
			<view class="tit">详情介绍</view>
			<view class="content">
				<rich-text :nodes="content"></rich-text>
			</view>
		</view>
		</view>
		
		<view class="goods_nav">
			<uni-goods-nav :fill="true"  :options="options" :button-group="buttonGroup"  @click="onClick" @buttonClick="buttonClick" ></uni-goods-nav>
		</view>
	</view>
</template>

<script>
	import uniGoodsNav from '@/components/uni-goods-nav/uni-goods-nav.vue'
	export default {
		components: {uniGoodsNav},
		data() {
			return {
				id:0,
				swipers:[],
				info:{},
				content:'',
				options: [
					{
						icon: 'https://img-cdn-qiniu.dcloud.net.cn/uniapp/uni-ui/goodsnav/kefu.png',
						text: '客服'
					}, 
					{
						icon: 'https://img-cdn-qiniu.dcloud.net.cn/uniapp/uni-ui/goodsnav/dianpu.png',
						text: '店铺'
					}, 
					{
						icon: 'https://img-cdn-qiniu.dcloud.net.cn/uniapp/uni-ui/goodsnav/carts.png',
						text: '购物车',
						info: 0
					}
				],
				buttonGroup: [
					{
						text: '加入购物车',
						backgroundColor: '#ff0000',
						color: '#fff'
					},
					{
						text: '立即购买',
						backgroundColor: '#ffa200',
						color: '#fff'
					}
				]
			}
		},
		methods: {
			async getDetailSwipers(){
			    const res = await this.$myRequest({
			      url:'/api/getthumimages/'+this.id
			    })
			    this.swipers = res.data.message
			},
			async getDetailInfo(){
			    const res = await this.$myRequest({
			      url:'/api/goods/getinfo/'+this.id
			    })
			    this.info = res.data.message[0]
			},
			async getDetailContent(){
			    const res = await this.$myRequest({
			      url:'/api/goods/getdesc/'+this.id
			    })
			    this.content = res.data.message[0].content
			},
			onClick (e) {
				uni.showToast({
					title: `点击${e.content.text}`,
					icon: 'none'
				})
			  },
			buttonClick (e) {
			    console.log(e)
			    this.options[2].info++
			}
		},
		onLoad(options){
		    this.id = options.id
		    this.getDetailSwipers()
			this.getDetailInfo()
			this.getDetailContent()
		}
	}
</script>

<style lang="scss">
	.goods_detail{
		swiper{
			height: 700rpx;
			image{
				width: 100%;
				height: 100%;
			}
		}
	}
	
	.box1 {
		padding: 20rpx;
		.price {
			font-size: 36rpx;
			color: $shop-color;
			line-height: 80rpx;
			text:nth-child(2){
				color: #ccc;
				font-size: 28rpx;
				text-decoration: line-through;
				margin-left: 20rpx;
			}
		}
		.goods_name {
			font-size: 32rpx;
			line-height: 60rpx;
		}
	}
	
	.line {
		height: 10rpx;
		width: 750rpx;
		background: #eee;
	}
	
	.box2 {
		padding: 0 20rpx;
		font-size: 32rpx;
		line-height: 80rpx;
	}
	
	.box3 {
		.tit {
			font-size: 32rpx;
			padding-left: 20rpx;
			border-bottom: 2rpx dashed #eee;
		}
		.content {
			padding: 20rpx;
			font-size: 28rpx;
			color: #333;
			padding-bottom: 100rpx;
		}
	}
	
	.goods_nav {
		position: fixed;
		bottom: 0;
		width: 100%;
	}
</style>
