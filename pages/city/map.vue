<template>
	<view>
		<map id="map" show-location="true" :controls="controls" @controltap="controltap" @markertap="markertap" :include-points="markers" :latitude="latitude" :longitude="longitude" :markers="markers" :polyline='polyline'></map>
		<!-- <view @click="tap">{{msg}}</view> -->
	</view>
</template>

<script>
	export default {
		data() {
			return {
				map:'',
				msg:'123',
			  id:0, // 使用 marker点击事件 需要填写id
				title: 'map',
				latitude:38.031341,
				longitude: 114.483629,
				markers: [{
					id:1,
					latitude: 38.031341,
					longitude: 114.483629,
					iconPath: '/static/ti1.png',
					width:20,
					height:20,
					callout:{content:'11',
					}
				}, {
					id:2,
					latitude: 38.025003,
					longitude: 114.484815,
					iconPath: '/static/ti1.png',
					width:20,
					height:20,
					callout:{content:'12',
					}
				}, {
					id:3,
					latitude: 38.041544,
					longitude: 114.521142,
					iconPath: '/static/ti1.png',
					width:20,
					height:20,
					callout:{content:'13',
					}
				}, {
					id:4,
					latitude: 38.049132,
					longitude: 114.518304,
					iconPath: '/static/ti1.png',
					width:20,
					height:20,
					callout:{content:'14',
					bgColor:'#fff'
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
					iconPath:'/static/ti1.png',//显示的图标	
					position:{//控件在地图的位置
						left:15,
						top:15,
						width:50,
						height:50
					},
					clickable:true
				},{//在地图上显示控件，控件不随着地图移动
					id:2,//控件id
					iconPath:'/static/ti1.png',//显示的图标	
					position:{//控件在地图的位置
						left:15,
						top:100,
						width:50,
						height:50
					},
					clickable:true
				}],
			}
		},
		methods: {
			tap(){
				this.axios.request({
					url:'api/user/login',
					method:'get',
					params:{account:'gl111',password:'123456',type:1}
				}).then(function({data}){
					console.log(data)
					uni.setStorage({
						key:'login',
						data:data.data
					})
				}).catch(err => {
					console.log(err)
				})
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
						item.iconPath = '/static/car.png'
					}else {
						item.iconPath = '/static/ti1.png'
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
		},
		onLoad() {
			uni.getStorage({
				key:'login',
				success: (res) => {
					console.log(res)
				},fail: (res) => {
					console.log(res)
				}
			})
			this.getLocation()
			this.map = uni.createMapContext('map',this)
		}
	}
</script>

<style>
	map {
		width: 750rpx;
		height: 600rpx;
		margin: 30rpx auto;
	}
</style>
