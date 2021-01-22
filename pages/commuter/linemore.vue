<template>
	<div>
		<div class="top flex">
			<image src="../../static/stop.png" mode="heightFix"></image>
			<div class="msg">
				<div class="title">{{msg.title}}<span>({{msg.num}}条线路)</span></div>
				<div class="distance">距离您	{{distance}}m</div>
			</div>
		</div>
		<div class="result">
			<block v-for='(item,index) in msg.line' :key="index">
				<litem :msg="item" :index="index" :star="true" @collect="collect"></litem>
			</block>
		</div>
	</div>
</template>

<script>
	import litem from '../components/line.vue'
	export default {
		components: {
			litem
		},
		data(){
			return {
				msg:{
					title:'海岸花园',
					num:4,
					line:[
						{
							line:'总部A',
							dest:'美的总部',
							time:2,
							num:1,
							distance:2.4,
							status:null
						},{
							line:'总部A',
							dest:'美的总部',
							time:2,
							num:1,
							distance:2.4,
							status:null
						}
					]
				},
				distance:200
			}
		},
		methods:{
			collect(data){
				// console.log(data)
				this.msg.line[data.index].status = !this.msg.line[data.index].status;
			}
		}
	}
</script>

<style scoped lang="scss">
	.top {
		height: 160rpx;
		font-size: 28rpx;
		justify-content: flex-start;
		padding: 0 30rpx;
		margin: 10rpx 0;
		background: #fff;
		image {
			height: 80rpx;
			margin-right: 26rpx;
		}
		.title {
			font-size: 32rpx;
			span {
				font-size: 28rpx;
				color: #999;
			}
		}
		.distance {
			color: #999;
			margin-top: 10rpx;
		}
	}
	
	.result {
		padding: 20rpx 30rpx;
		/deep/ .litem:last-child .item {
			border: none;
		}
	}
</style>
