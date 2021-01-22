<template>
	<div class="litem" :class="shou?'shou':''">
		<div class="item flex" >
			<div class="map" @click="map"></div>
			<div class="left">
				<div class="lt ellip"><image mode="widthFix" v-if="car" src="../../static/tab11.png"></image>{{msg.line}}</div>
				<div class="lb ellip">开往 {{msg.dest}}</div>
			</div>
			<div class="right" :class="star?'star':''">
				<div class="rt">{{msg.time}}分钟</div>
				<div class="rb">{{msg.num}}站/{{msg.distance}}km</div>
				<!-- <image  src="../../static/ti4.png" mode="widthFix"></image> -->
				<u-icon class="image" @click="collect" v-if="star" :index="datum" name="star-fill" :color="msg.status?'#FDAB11':'#D2D2D2'" size="44"></u-icon>
			</div>
		</div>
		<div class="stop" v-if="stop">在 {{msg.origin}} 站上车</div>
		<div class="stop shou flex" v-if="shou"><span>站点 {{msg.origin}}</span><image src="../../static/ti4.png" mode="widthFix"></image></div>
	</div>
</template>

<script>
	export default{
		props:['msg','index','car','stop','star','shou'],
		methods:{
			collect(data){
				this.$emit('collect',JSON.parse(data))
			},
			map(){
				uni.navigateTo({
					url:'../commuter/map'
				})
			},
		},
		computed:{
			datum(){
				return JSON.stringify({index:this.$props.index,id:this.$props.msg.id})
			}
		}
	}
</script>

<style scoped lang="scss">
	.litem {
		background: #fff;
		border-radius: 20rpx;
	}
	.shou {
		margin-bottom: 20rpx;
	}
	.item {
		height: 130rpx;
		margin: 0 30rpx;
		border-bottom: 1px solid #e5e5e5;
		position: relative;
		
		.map {
			position: absolute;
			width: calc(100% - 40rpx);
			height: 100%;
		}
		
		.rt {
			color: #3875F6;
			text-align: right;
		}
		.lb,.rb{
			margin-top: 10rpx;
			color: #999;
		}
		.lt,.lb {
			width: 300rpx;
			display: flex;
			align-items: center;
		}
		
		image {
			width: 32rpx;
			height: 32rpx;
			margin-right: 20rpx;
		}
	}
	.stop {
		height: 85rpx;
		line-height: 85rpx;
		margin: 0 30rpx;
	}
	.stop.shou {
		color: #999;
		position: relative;
		top: -15rpx;
		height: 50rpx;
		line-height: 50rpx;
		background-color: #fff;
		image {
			width: 40rpx;
			height: 40rpx;
		}
	}
	.star {
		padding-right: 60rpx;
		position: relative;
	}
	.star .image {
		width: 40rpx;
		position: absolute;
		right: 0;
		top:50%;
		transform: translateY(-50%);
	}
</style>
