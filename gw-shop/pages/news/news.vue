<template>
	<view class="news">
		<news-item @itemClick="goDetail" :list="newsDetail"></news-item>
	</view>
</template>

<script>
	import newsItem from '../../components/news-item.vue'
	export default {
		data() {
			return {
				newsDetail:[]
			}
		},
		methods: {
			async getNewsDetail(id){
			    const res = await this.$myRequest({
			      url: '/api/getnewslist'
			    })
			    console.log(res)
			    this.newsDetail = res.data.message
			},
			goDetail (id) {
				uni.navigateTo({
					url:'/pages/new-detail/new-detail?id=' + id
				})
			}
		},
		components:{"news-item":newsItem},
		onLoad () {
			this.getNewsDetail()
		}
	}
</script>

<style lang="scss">
	.news{
		
	}

</style>
