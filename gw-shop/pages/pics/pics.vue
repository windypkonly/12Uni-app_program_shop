<template>
	<view class="pics">
		<scroll-view class="left" scroll-y>
			<view :class="active === index?'active':''" 
				  @click="leftClickHandle(index,item.id)"
			      v-for="(item,index) in cates" 
				  :key="item.id">{{item.title}}</view>
		</scroll-view>
		<scroll-view class="right" scroll-y >
			<view class="item" v-for="item in secondData" :key="item.id">
				<image @click="previewImg(item.img_url)" :src="item.img_url"></image>
				<text>{{item.title}}</text>
			</view>
			<text v-if="secondData.length === 0">暂无数据，点击查看其它分类</text>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				cates: [],
				active: 0,
				secondData: []
			}
		},
		methods: {
			async getPicsCate () {
				const res = await this.$myRequest({
					url:'/api/getimgcategory'
				})
				this.cates = res.data.message
				this.leftClickHandle(0,this.cates[0].id)
			},
			async leftClickHandle (index,id) {
				this.active = index
				//获取右侧相册数据
				const res = await this.$myRequest({
					url: '/api/getimages/' + id
				})
				this.secondData = res.data.message
			},
			previewImg (current) {
				const urls = this.secondData.map(item => {
					return item.img_url
				})
				uni.previewImage({
					current,
					urls
				})
			}
		},
		onLoad () {
			this.getPicsCate()
		}
	}
</script>

<style lang="scss">
	page {
		height: 100%;
	}
	.pics {
		display: flex;
		height: 100%;
		.left {
			width: 200rpx;
			height: 100%;
			border-right: 1px dashed #eee;
			view {
				height: 120rpx;
				line-height: 120rpx;
				color: #333;
				text-align: center;
				font-size: 30rpx;
				border-top: 1px dashed #eee;
			}
			.active {
				background: $shop-color;
				color: #fff;
			}
		}
		.right {
			height: 100%;
			width: 520rpx;
			margin: 10rpx auto;
			.item {
				image {
					width: 520rpx;
					height: 520rpx;
					border-radius: 10rpx;
				}
				text {
					font-size: 30rpx;
					line-height: 60rpx;
				}
			}
		}
	}

</style>
