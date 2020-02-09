<template>
	<view>
		<view class="goods_list">
			<goods-list :goods="goods" @goodsItemClick="goGoodsDetail"></goods-list>
			<view class="over_line" v-if="flag">----------我是有底线的----------</view>
		</view>
		
	</view>
</template>

<script>
	import goodsList from "../../components/goods-list.vue";
	export default {
		data () {
			return {
				pageindex:1,
				goods: [],
				flag:false
				
			}
		},
		components: {
			"goods-list": goodsList
		},
		methods: {
			async getGoods (callBack) {
				const res = await this.$myRequest({
					url: '/api/getgoods?pageindex=' + this.pageindex
				})
				this.goods = [...this.goods,...res.data.message]
				callBack && callBack()
			},
			goGoodsDetail (id) {
				uni.navigateTo({
					url: '/pages/goods-detail/goods-detail?id=' +id
				})
			}
		},
		
		onLoad () {
			this.getGoods()
		},
		onReachBottom () {
			if(this.goods.length < this.pageindex*10) return this.flag = true
			this.pageindex++
			this.getGoods()
		},
		onPullDownRefresh() {
		  this.goods = []
		  this.pageindex = 1
		  this.flag = false 
		  setTimeout(()=>{
		    this.getGoods(()=>{
		      uni.stopPullDownRefresh()
		    })
		  },1000)
		}
	}
</script>

<style lang="scss">
	.goods_list {
		background: #eee;
	}
	.over_line {
		color: #C0C0C0;
		width: 100%;
		height: 100rpx;
		line-height: 100rpx;
		text-align: center;
		font-size: 28rpx;
	}
</style>
