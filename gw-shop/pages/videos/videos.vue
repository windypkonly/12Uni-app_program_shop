<template>
	<view class="videos">
		<view class="videos-item" v-for="(item,index) in videos" :key="index">
			<view class="title">{{item.title}}</view>
			<video class="content" :src="item.url" controls></video>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				videos:[
					{
						title:"uni-app",
						url:"https://img.cdn.aliyun.dcloud.net.cn/guide/uniapp/%E7%AC%AC1%E8%AE%B2%EF%BC%88uni-app%E4%BA%A7%E5%93%81%E4%BB%8B%E7%BB%8D%EF%BC%89-%20DCloud%E5%AE%98%E6%96%B9%E8%A7%86%E9%A2%91%E6%95%99%E7%A8%8B@20181126.mp4"
					}
				]
			}
		},
		methods: {
			
		}
	}
</script>

<style lang="scss">
	.videos {
		.videos-item {
			margin: 15rpx;
			.title {
				margin-bottom: 15rpx;
				font-size: 36rpx;
			}
			.content {
				width: 720rpx;
				height: 480rpx;
			}
		}
	}
</style>
