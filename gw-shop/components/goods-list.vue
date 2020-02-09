<template>
	<view class="goods_list">
		<view class="goods_item" 
		v-for="item in goods" 
		:key="item.id" 
		@click="navigator(item.id)">
			<image :src="item.img_url"></image>
			<view class="price">
				<text>{{item.sell_price}}</text>
				<text>{{item.market_price}}</text>
			</view>
			<view class="name">{{item.title}}</view>
		</view>
	</view>
</template>

<script>
	export default {
		props:{
			goods:Array
		},
		methods:{
			navigator (id) {
				this.$emit('goodsItemClick',id)
			}
		}
	}
</script>

<style lang="scss">
	.goods_list {
		background: #eee;
		display: flex;
		padding: 0 15rpx;
		justify-content: space-between;
		overflow: hidden;
		flex-wrap: wrap;
		.goods_item {
			width: 355rpx;
			margin-bottom: 15rpx;
			background: #fff;
			padding: 20rpx;
			box-sizing: border-box;
			image{
				height: 300rpx;
				width: 100%;
				display: block;
				margin: 20rpx auto;
			}
			.price{
				font-size: 36rpx;
				color: red;
				padding: 16rpx 0;
				text:nth-child(2){
					color: #ccc;
					text-decoration: line-through;
					margin-left: 20rpx;
					font-size: 26px;
				}
			}
			.name {
				font-size: 28rpx;
				
			}
		}
	}
</style>
