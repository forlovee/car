<template>
	<div class="main">
		<div class="line flex">
			<div class="ll">
				<div class="title">{{msg.line}}</div>
				<div class="ft">{{msg.from}} 至 {{msg.to}}</div>
			</div>
			<div class="lr">
				<u-icon class="image" @click="collect" :index="msg.id" name="star-fill" :color="msg.status?'#FDAB11':'#D2D2D2'" size="44"></u-icon>
				<div class="tip">{{msg.status?'已收藏':'收藏'}}</div>
			</div>
		</div>
		<div class="stop">
			<div class="tip flex">
				<image src="../../static/tic2.png" mode="heightFix"></image>
				到站：2分钟
			</div>
			<div class="chart">
				<div class="scroll">
					<image class="car" src="../../static/car.png" mode="heightFix"></image>
					<div class="item" :class="chartIndex==index?'active':''" @click="chartChange(index)" v-for="(item,index) in chart" :key="item">
						<div class="icon">
							<div class="il" v-if="index!=0"></div>
							<image :src="chartIndex==index?'../../static/line.png':'../../static/c-now.png'" mode="heightFix"></image>
							<div class="ir" v-if="index!=chart.length - 1"></div>
						</div>
						<div class="title">{{item}}</div>
					</div>
				</div>
			</div>
		</div>
		<div class="map">
			<div class="tip">我的行程</div>
			<div class="pred">本次乘车约3分钟，共3站</div>
			<map id="map" show-location="true" :controls="controls" @controltap="controltap" @markertap="markertap" :include-points="markers" :latitude="latitude" :longitude="longitude" :markers="markers" :polyline='polyline'></map>
			<div class="items">
				<div class="item flex"><div class="il">候车</div><div class="ir">最近一班2分钟</div></div>
				<div class="item flex"><div class="il">乘车</div><div class="ir">共3站/39分钟</div></div>
				<div class="item flex"><div class="il">目的地</div><div class="ir">预计8:00到达</div></div>
			</div>
		</div>
		<div class="linemsg">
			<div class="item">线路里程：12公里，约39分钟</div>
			<div class="item flex"><div class="il">班车座位：43/43</div><div class="ir">车牌号：粤E08110</div></div>
		</div>
	</div>
</template>

<script>
	export default {
		data(){
			return {
				map:'', 
				msg:{
					id:1,
					line:'总部A',
					from:'海岸花园',
					to:'美的总部',
					status:null,
				},
				chart:['海岸花园','海岸花园','海岸花园','海岸花园','海岸花园','1111111111111','1111111111111'],
				chartIndex:0,
				latitude:38.031341,
				longitude: 114.483629,
				markers: [{
					id:1,
					latitude: 38.031341,
					longitude: 114.483629,
					iconPath: '/static/c-end.png',
					width:20,
					height:20,
					callout:{content:'海岸花园',
					bgColor:'#3875F6',
					color:'#fff',
					display:'ALWAYS',
					padding:3,
					borderRadius:20
					}
				}, {
					id:2,
					latitude: 38.025003,
					longitude: 114.484815,
					iconPath: '/static/line.png',
					width:20,
					height:20,
					callout:{content:'海岸花园',
					bgColor:'#3875F6',
					color:'#fff',
					display:'ALWAYS',
					padding:3,
					borderRadius:20
					}
				}, {
					id:3,
					latitude: 38.041544,
					longitude: 114.521142,
					iconPath: '/static/line.png',
					width:20,
					height:20,
					callout:{content:'海岸花园',
					bgColor:'#3875F6',
					color:'#fff',
					display:'ALWAYS',
					padding:3,
					borderRadius:20
					}
				}, {
					id:4,
					latitude: 38.049132,
					longitude: 114.518304,
					iconPath: '/static/c-now.png',
					width:20,
					height:20,
					callout:{content:'海岸花园',
					bgColor:'#3875F6',
					color:'#fff',
					display:'ALWAYS',
					padding:3,
					borderRadius:20
					}
				}],
				polyline:[
					{
						points:[
							{latitude: 38.031341,longitude: 114.483629},
							{latitude: 38.025003,longitude: 114.484815},
							{latitude: 38.041544,longitude: 114.521142},
							{latitude: 38.049132,longitude: 114.518304},
						],
						color:'#f40',
						width:4
					}
				],
				controls:[{//在地图上显示控件，控件不随着地图移动
					id:1,//控件id
					// iconPath:'/static/ti1.png',//显示的图标	
					position:{//控件在地图的位置
						left:15,
						top:15,
						width:50,
						height:50
					},
					clickable:true
				},{//在地图上显示控件，控件不随着地图移动
					id:2,//控件id
					// iconPath:'/static/ti1.png',//显示的图标	
					position:{//控件在地图的位置
						left:15,
						top:100,
						width:50,
						height:50
					},
					clickable:true
				}]
			}
		},
		onLoad() {
			this.getLocation()
			this.map = uni.createMapContext('map',this)
		},
		methods:{
			chartChange(index){
				this.chartIndex = index;
			},
			collect(data){
				this.msg.status = !this.msg.status;
			},
			controltap(e){
				console.log(e)
				let that = this;
				switch (e.detail.controlId){
					case 1:
						this.getLocation()
						break;
					case 2:
						this.map.includePoints({
							points:that.markers
						})
				}
			},
			markertap(e){
				console.log(e)
				let result = JSON.parse(JSON.stringify(this.markers))
				result.forEach(function(item){
					if(item.id == e.detail.markerId){
						item.iconPath = '/static/c-now.png'
					}else {
						item.iconPath = '/static/line.png'
					}
				})
				console.log(result)
				this.markers = result;
			},
			getLocation(){
				let that = this;
				uni.getLocation({
					type: 'gcj02',
					success:res=>{
						console.log(res)
						if(res){
							that.latitude = res.latitude;
							that.longitude = res.longitude;
							that.map.moveToLocation({
								latitude:res.latitude,
								longitude:res.longitude
							})
						}
					},
					fail: (res) => {
						alert('请打开定位功能后重新进入')
					}
				})
			}
		}
	}
</script>

<style scoped lang="scss">
	.main {
		padding: 0 30rpx;
		font-size: 28rpx;
	}
	.line {
		height: 160rpx;
		.title {
			font-size: 36rpx;
			margin-bottom: 10rpx;
		}
		.lr {
			text-align: center;
		}
		.tip {
			color: #999;
		}
	}
	.stop {
		padding: 0 30rpx;
		border-radius: 12rpx;
		background: #fff;
		
		.tip {
			line-height: 90rpx;
			justify-content: flex-start;
			border-bottom: 1rpx solid #e5e5e5;
			image {
				height: 48rpx;
				margin-right: 20rpx;
			}
		}
		.chart {
			padding: 80rpx 0 40rpx;
			position: relative;
			overflow: scroll;
			.scroll {
				width: max-content;
				overflow-x: scroll;
			}
			.car {
				height: 34rpx;
				position: absolute;
				top: 25rpx;
				left: 45rpx;
			}
			.item {
				display: inline-block;
				width: 140rpx;
				.icon {
					position: relative;
					text-align: center;
					image {
						height: 40rpx;
						position: relative;
						z-index: 2;
					}
					.il,.ir {
						position: absolute;
						top:15rpx;
						width: 70rpx;
						height: 10rpx;
						background: #3875F6;
					}
					.il {
						left: 0;
					}
					.ir {
						right: 0;
					}
				}
				.title {
					writing-mode: vertical-lr;
					margin: auto;
				}
				&.active .title {
					color: #3875F6;
				}
			}
		}
	}
	.map {
		padding: 0 30rpx;
		border-radius: 12rpx;
		background: #fff;
		margin: 20rpx 0;
		.tip {
			font-size: 32rpx;
			line-height: 90rpx;
		}
		.pred {
			padding-left: 25rpx;
			height: 80rpx;
			line-height: 80rpx;
			color: #fff;
			background: #F1AE3F;
			border-radius: 12rpx;
			margin: 0 0 20rpx;
		}
		map {
			width: 630rpx;
			height: 300rpx;
		}
		.items {
			.item {
				line-height: 80rpx;
				.il {
					padding-left: 40rpx;
				}
				.ir {
					color: #3875F6;
				}
			}
		}
	}
	.linemsg {
		padding: 0 30rpx;
		border-radius: 12rpx;
		background: #fff;
		.item {
			height: 90rpx;
			line-height: 90rpx;
			
			&:first-child {
				border-bottom: 1rpx solid #e5e5e5;
			}
		}
	}
</style>
