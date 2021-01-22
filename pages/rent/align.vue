<template>
	<div class="main">
		<swiper class="swiper" :indicator-dots="true" :autoplay="true" indicator-active-color="#fff" circular>
			<swiper-item v-for="item in swiper" :key="index">
				<image :src="item" mode=""></image>
			</swiper-item>
		</swiper>
		<div class="tip">必填信息</div>
	</div>
</template>

<script>
	export default {
		data(){
			return {
				swiper:[
					'../../static/banner.png','../../static/banner.png','../../static/banner.png'
				],
			}
		}
	}
</script>

<style scoped lang="scss">
	.main {
		padding: 30rpx ;
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
		font-size: 36rpx;
	}
</style>
