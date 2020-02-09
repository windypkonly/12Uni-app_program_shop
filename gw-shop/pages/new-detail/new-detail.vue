<template>
	<view class="news_detail">
		<view class="news_title">{{newsDetail.title}}</view>
		<view class="info">
			<text>发表时间：{{newsDetail.add_time | formatDate}}</text>
			<text>浏览：{{newsDetail.click}}</text>
		</view>
		<view class="content">
			<rich-text :nodes="newsDetail.content"></rich-text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				id:0,
				newsDetail: {}
			}
		},
		methods: {
			async getNewsDetail(id){
			    const res = await this.$myRequest({
			      url: '/api/getnew/' + this.id
			    })
			    this.newsDetail = res.data.message[0]
			}
		},
		 onLoad (options){
			this.id = options.id
		    this.getNewsDetail()
		}
	}
</script>

<style lang="scss">
	.news_detail {
		padding: 15rpx;
		.news_title{
			text-align: center;
			font-size: 32rpx;
		}
		.info{
			margin: 15rpx;
			font-size: 28rpx;
			display: flex;
			justify-content: space-between;
		}
	}
</style>
