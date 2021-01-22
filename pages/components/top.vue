<template>
	<div>
		<!--顶部nav-->
		<view class="status_bar flex"><i class="uni-btn-icon" style="color: rgb(0, 0, 0); font-size: 27px;"></i><view class="title">{{title}}</view></view>
		
	</div>
</template>

<script>
	export default {
		props:['title']
	}
</script>

<style scoped>
	.status_bar {
		position: fixed;
		left: 0;
		top: 0;
		z-index: 100;
	    height: calc(44px + env(safe-area-inset-top));
		background: #fff;
	    width: 100%;
		padding: 0 15rpx;
	}
	.title {
		position: absolute;
		width: 100%;
		left: 0;
		font-weight: 700;
		font-size: 16px;
		line-height: 30px;
		text-align: center;
		overflow: hidden;
		white-space: nowrap;
		text-overflow: ellipsis;
	}
	
</style>
