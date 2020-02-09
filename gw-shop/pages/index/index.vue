<template>
	<view class="home">
		<!-- 1 轮播图 -->
		<swiper class="swiper" indicator-dots :autoplay="true" :interval="2000" circular>
		  <swiper-item v-for="item in swipers" :key="item.id">
		    <image :src="item.img"></image>
		  </swiper-item>
		</swiper>
		
		<!-- 2 导航栏 -->
		<view class="nav">
		  <view class="item" v-for="(item,index) in navs" :key="index" @click="goNavigator(item.path)">
			<view :class="item.icons"></view>
		    <text>{{item.title}}</text>
		  </view>
		</view>
		
		<!-- 3 推荐商品 -->
		<goods-list :goods="goods" @goodsItemClick="goGoodsDetail"></goods-list>
	</view>
</template>

<script>
	import goodsList from "../../components/goods-list.vue"
	export default {
		data() {
			return {
				swipers:[],
				goods:[],
				navs: [
				  {
				    icons: "iconfont icon-ziyuan",
				    title: "数码产品",
				    path: "/pages/goods/goods"
				  },
				  {
				    icons: "iconfont icon-tupian",
				    title: "社区图片",
				    path: "/pages/pics/pics"
				  },
				  {
				    icons: "iconfont icon-guanyuwomen",
				    title: "联系我们",
				    path: "/pages/contact/contact"
				  },
				  {
				    icons: "iconfont icon-shipin",
				    title: "学习视频",
				    path: "/pages/videos/videos"
				  }
				]
			}
		},
		onLoad() {
			this.getSwipers()
			this.getGoods()
		},
		components: {
		  "goods-list":goodsList
		},
		methods: {
			// 1 获取轮播图数据
			async getSwipers () {
			    const res = await this.$myRequest({
			      method: 'GET',
			      url: '/api/getlunbo'
			    })
			    this.swipers = res.data.message
			},
			// 2 获取推荐商品数据
			async getGoods () {
			  const res = await this.$myRequest({
			    url: '/api/getgoods?pageindex=1'
			  })
			  this.goods = res.data.message
			},
			// 导航点击跳转处理函数
			goNavigator (url) {
			  uni.navigateTo({
			    url
			  })
			},
			// 导航到商品详情页
			goGoodsDetail (id) {
				uni.navigateTo({
					url: '/pages/goods-detail/goods-detail?id=' +id
				})
			}
		}
	}
</script>

<style lang="scss">
	.home{
		swiper{
			height: 380rpx;
			image{
				width: 750rpx;
				height: 380rpx;
			}
		}
		.nav{
		  display: flex;
		  align-items: center;
		  .item{
		    width: 25%;
		    text-align: center;
		    view{
		      background: $shop-color;
		      line-height: 120rpx;
		      width: 120rpx;
		      height: 120rpx;
		      border-radius: 90px;
		      margin:10px auto;
		    }
		    text{
		      font-size: 15px;
		    }
		  }
		  .iconfont{
		    font-size: 25px;
		    color: #fff;
		    height: 50px;
		  }
		  .icon-tupian{
		    font-size: 20px;
		  }
		}
	}
	
	
</style>
