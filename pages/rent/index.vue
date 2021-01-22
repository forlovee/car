<template>
	<div class="main">
		<top title="租车服务"></top>
		<swiper class="swiper" :indicator-dots="true" :autoplay="true" indicator-active-color="#fff" circular>
			<swiper-item v-for="(item,index) in swiper" :key="index">
				<image :src="item" mode=""></image>
			</swiper-item>
		</swiper>
		<div class="tip">租车服务</div>
		<div class="turn flex">
			<div class="item" v-for="(item,index) in turn" :key="index" @click="onTurn(item.url)">
				<image :src="item.image" mode="heightFix"></image>
				<div class="title">{{item.title}}</div>
			</div>
		</div>
	</div>
</template>

<script>
	import top from '../components/top.vue'
	export default {
		components: {
			top
		},
		data(){
			return {
				swiper:[
					'../../static/banner.png','../../static/banner.png','../../static/banner.png'
				],
				turn:[
					{image:'../../static/rent1.png',title:'自驾',url:'./self'},
					{image:'../../static/rent2.png',title:'随驾',url:'./align'},
					{image:'../../static/rent3.png',title:'我的租车',url:'./rentlist'}
				]
			}
		},
		methods:{
			onTurn(url){
				uni.navigateTo({
					url
				})
			}
		}
	}
</script>

<style scoped lang="scss">
	.main {
		padding: 30rpx ;
		padding-top: calc(50px + env(safe-area-inset-top));
	}
	swiper {
		height: 300rpx;
		width: 690rpx;
		background: #FFFFFF;
		border-radius: 20rpx;
		image {
			height: 300rpx;
			width: 690rpx;
		}
	}
	.tip {
		line-height: 90rpx;
		font-size: 32rpx;
	}
	.turn {
		height: 200rpx;
		justify-content: space-around;
		text-align: center;
		background: #FFFFFF;
		border-radius: 20rpx;
		image {
			height: 88rpx;
			margin-bottom: 6rpx;
		}
	}
</style>
