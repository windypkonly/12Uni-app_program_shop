<template>
	<view>
		<view class="news_item" 
		@click="navigator(item.id)" 
		v-for="item in list" 
		:key="item.id">
			<image :src="item.img_url"></image>
			<view class="content">
				<view class="tit">{{item.title}}响</view>
				<view class="info">
					<text>发表时间：{{item.add_time | formatDate}}</text>
					<text>浏览：{{item.click}}</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props:['list'],
		filters:{
			formatDate(date) {
				const nDate = new Date(date)
				const year = nDate.getFullYear()
				const month = nDate.getMonth().toString().padStart(2,0)
				const day = nDate.getDay().toString().padStart(2,0)
				return year + '-' + month + '-' + day
			}
		},
		methods:{
			navigator(id){
				this.$emit('itemClick',id)
			},
		}
	}
	
</script>

<style lang="scss">
	.news_item{
		display: flex;
		padding: 10rpx 20rpx;
		border-bottom: 1rpx dashed $shop-color;
		image{
			width: 300rpx;
			height: 150rpx;
		}
		.content {
			padding: 10rpx 20rpx;
			position: relative;
			.tit{
				font-size: 30rpx;
			}
			.info{
				font-size: 26rpx;
				position: absolute;
				left: 20rpx;
				bottom: 10rpx;
				text:nth-child(2){
					margin-left: 40rpx;
				}
			}
		}
	}
</style>
