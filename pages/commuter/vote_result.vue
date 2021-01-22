<template>
	<div>
		<block v-if="true">
			<image src="../../static/success.png" mode="heightFix"></image>
			<div class="title">投票成功，感谢您的参与</div>
			<div class="button" @click="confirm">确定</div>
		</block>
		<block v-else>
			<image src="../../static/success.png" mode="heightFix"></image>
			<div class="title">投票失败，请重新参与投票</div>
			<div class="button" @click="confirm">重新投票</div>
		</block>
	</div>
</template>

<script>
	export default {
		data(){
			return {
				
			}
		},
		methods:{
			confirm(){
				uni.switchTab({
					url:'./index'
				})
			}
		}
	}
</script>

<style scoped lang="scss">
	image {
		display: block;
		height: 180rpx;
		margin: 30rpx auto;
	}
	.title {
		text-align: center;
	}
	.button {
		width: 520rpx;
		height: 90rpx;
		line-height: 90rpx;
		border-radius: 12rpx;
		background: var(--blue);
		text-align: center;
		color: #fff;
		margin: 40rpx auto;
	}
</style>
