<template>
	<div class="main">
		<swiper class="swiper" :indicator-dots="true" :autoplay="true" indicator-active-color="#fff" circular>
			<swiper-item v-for="item in swiper" :key="index">
				<image :src="item" mode=""></image>
			</swiper-item>
		</swiper>
		<div class="tip">租车服务</div>
		<div class="msg">
			<div class="item flex">
				<div class="il">车型</div>
				<div class="ir">
					<view class="uni-list">
						<view class="uni-list-cell">
							<view class="uni-list-cell-db">
								<picker mode="time" :value="time1" start="00:00" end="23:59" @change="bindTimeChange1">
									<view class="uni-input">{{time1?time1:'请选择车型'}}</view>
								</picker>
							</view>
						</view>
					</view>
					<span class="iconfont icon-weibiaoti34"></span>
				</div>
			</div>
			<div class="item flex">
				<div class="il">座位数</div>
				<div class="ir">
					<view class="uni-list">
						<view class="uni-list-cell">
							<view class="uni-list-cell-db">
								<picker mode="time" :value="time1" start="00:00" end="23:59" @change="bindTimeChange1">
									<view class="uni-input">{{time1?time1:'请选择座位数'}}</view>
								</picker>
							</view>
						</view>
					</view>
					<span class="iconfont icon-weibiaoti34"></span>
				</div>
			</div>
			<div class="item flex">
				<div class="il">出行日期</div>
				<div class="ir">
					<view class="uni-list">
						<view class="uni-list-cell">
							<view class="uni-list-cell-db">
								<picker mode="time" :value="time1" start="00:00" end="23:59" @change="bindTimeChange1">
									<view class="uni-input">{{time1?time1:'请选择起租日期'}}</view>
								</picker>
							</view>
						</view>
					</view>
					<span class="iconfont icon-weibiaoti34"></span>
				</div>
			</div>
			<div class="item flex">
				<div class="il">预计还车时间</div>
				<div class="ir">
					<view class="uni-list">
						<view class="uni-list-cell">
							<view class="uni-list-cell-db">
								<picker mode="time" :value="time1" start="00:00" end="23:59" @change="bindTimeChange1">
									<view class="uni-input">{{time1?time1:'请选择还车时间'}}</view>
								</picker>
							</view>
						</view>
					</view>
					<span class="iconfont icon-weibiaoti34"></span>
				</div>
			</div>
		</div>
		<div class="count">预计时间 <span>{{day}}</span> 天</div>
		<div class="msg">
			<div class="item flex">
				<div class="il">联系人</div>
				<input type="text" placeholder="请输入您的真实姓名">
			</div>
			<div class="item flex">
				<div class="il">联系电话</div>
				<input type="text" placeholder="请输入你的联系电话号码">
			</div>
		</div>
	</div>
</template>

<script>
	export default {
		data(){
			return {
				swiper:[
					'../../static/banner.png','../../static/banner.png','../../static/banner.png'
				],
				
				day:0, // 用车时间
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
		font-size: 32rpx;
	}
	.count {
		line-height: 90rpx;
		padding-left: 30rpx;
		span {
			color: #EB5232;
			margin: 0 10rpx;
		}
	}
	.msg {
		padding: 0 30rpx;
		border-radius: 12rpx;
		background: #fff;
		.item {
			height: 90rpx;
			.il {
				min-width: 140rpx;
			}
			.ir {
				color: #666;
				display: flex;
				align-items: center;
				span {
					padding-top: 6rpx;
				}
			}
		}
		.item + .item {
			border-top: 1px solid #eee;
		}
		input {
			flex: 1;
			// text-align: right;
			color: #999;
		}
	}
</style>
