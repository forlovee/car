<template>
	<div class="main">
		<top title="首页"></top>
		<login v-if="!loginStatus" @login="login" :fault="fault"></login>
		<div v-else class="index">
			<div class="top">
				<!-- <div class="locate"><image src="../../static/tic1.png" mode="heightFix"></image>美林海岸花园...</div> -->
				<div class="button flex">
					<div class="item" v-for="(item,index) in button" :key="index" @click='turn(item.url)'>
						<image :src="item.image" mode="heightFix"></image>
						<div class="title">{{item.title}}</div>
					</div>
				</div>
			</div>
			<div class="bot">
				<div class="tip">附近站点</div>
				<block v-for="(block,index) in list" :key="index">
					<div class="block">
						<div class="dest flex" @click="more">
							<div><image mode="heightFix" src="../../static/stop-o.png"></image><span class="ellip">{{block.title}}</span>（{{block.num}}条线路）</div>
							<u-icon name="arrow-right" size="30"></u-icon>
						</div>
						<block v-for='(item,index) in block.line' :key="index">
							<litem :msg="item"></litem>
						</block>
					</div>
				</block>
			</div>
		</div>
	</div>
</template>

<script>
	import login from '../login/login'
	import litem from '../components/line.vue'
	import top from '../components/top.vue'
	export default {
		components: {
			login,
			litem,
			top
		},
		data(){
			return {
				fault:false,
				loginStatus:false,
				button:[
					{image:'../../static/ti1.png',title:'站点查询',url:'../commuter/zhandian'},
					{image:'../../static/ti2.png',title:'线路查询',url:'../commuter/xianlu'},
					{image:'../../static/ti3.png',title:'新线路需求',url:'../commuter/xuqiu'},
					{image:'../../static/ti4.png',title:'收藏',url:'../commuter/shoucang'},
				],
				list:[
					{
						title:'海岸花园',
						num:4,
						line:[
							{
								line:'总部A',
								dest:'美的总部',
								time:2,
								num:1,
								distance:2.4
							},{
								line:'总部A',
								dest:'美的总部',
								time:2,
								num:1,
								distance:2.4
							}
						]
					}
				]
			}
		},
		onLoad() {
			// 检查登录状态
			let that = this;
			uni.getStorage({
				key:'loginStatus',
				success(res){
					let expire = new Date().valueOf() - res.data.userinfo.expiretime * 1000;
					if(expire < 0){
						that.loginStatus = true
						// uni.getLocation({
						// 	success: (res) => {
						// 		console.log(res)
						// 	},
						// 	fail: (res) => {
						// 		console.log(res)
						// 	}
						// })
						uni.chooseLocation({
							success(res) {
								console.log(res)
							}
						})
					}
				}
			})
		},
		methods:{
			// 登录成功保存登录状态
			login(data){
				console.log(data)
				let that = this;
				this.axios.request({
					url:'api/user/login',
					method:'get',
					params:{account:data.name,password:data.number,type:1}
					// params:{account:'gl111',password:'123456',type:1}
				}).then(function({data}){
					console.log(data)
					if(data.code == 1){
						uni.showToast({
							title:data.msg
						})
						setTimeout(()=>{
							that.loginStatus = true;
							uni.setStorage({
								key:'loginStatus',
								data:data.data
							})
							uni.getLocation({
								success: (res) => {
									console.log(res)
								}
							})
							uni.chooseLocation({
								success(res) {
									console.log(res)
								}
							})
						},1000)
					}else {
						that.fault = true
					}
				}).catch(err => {
					console.log(err)
				})
			},
			turn(url){
				uni.navigateTo({
					url
				})
			},
			more(){
				uni.navigateTo({
					url:'linemore'
				})
			}
		}
	}
</script>

<style scoped lang="scss">
	page {
		padding-top: calc(44px + env(safe-area-inset-top));
	}
	.index {
		color: #333;
	}
	.top {
		position: sticky;
		top: 0;
		background: #fff;
		padding: 10rpx 30rpx 0;
		
		.locate {
			font-size: 32rpx;
			image {
				height: 32rpx;
				margin-right: 10rpx;
			}
		}
		.button{
			text-align: center;
			height: 200rpx;
			.item {
				min-width: 110rpx;
			}
			image {
				height: 60rpx;
			}
		}
	}
	
	.bot {
		padding: 0 30rpx;
		.tip {
			font-size: 32rpx;
			margin: 30rpx 0;
		}
		.block {
			background:#fff;
			.dest {
				> div {
					display: flex;
					align-items: center;
				}
				margin: 0 30rpx;
				height: 80rpx;
				color: #999;
				border-bottom: 1px solid #e5e5e5;
				span {
					color: #333;
					max-width: 190rpx;
				}
				image {
					height: 44rpx;
					margin-right: 15rpx;
				}
			}
			/deep/ .litem:last-child .item {
				border: none;
			}
		}
	}
	
</style>
