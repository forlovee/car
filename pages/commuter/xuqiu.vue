<template>
	<div class="main">
		<div class="tip">新线路规划</div>
		<div class="block" v-for="(line,index) in block">
			<div class="line flex">
				<span>{{line.title}}</span>
				<div class="select">
					<u-radio-group v-model="index">
						<u-radio active-color="red">选择</u-radio>
					</u-radio-group>
				</div>
			</div>
			<div class="tips">路线相关站点（可多选）</div>
			<div class="stop">
				<div class="item active" v-for="item in line.line">{{item}}</div>
			</div>
		</div>
		<div class="tip">需求征集</div>
		<div class="msg">
			<div class="item flex">
				<div class="il">企业名称</div>
				<input type="text" placeholder="请输入">
			</div>
			<div class="item flex">
				<div class="il">出行类型</div>
				<div class="ir" @click="onType">{{type_on?type_on:'请选择'}} <span class="iconfont icon-weibiaoti34"></span></div>
			</div>
		</div>
		<div class="msg moreMsg" v-if="type_on">
			<div class="title">{{type_on}}</div>
			<div class="item flex">
				<div class="il">下车时间{{type_index == 2?'(去)':''}}</div>
				<div class="ir">
					<view class="uni-list">
						<view class="uni-list-cell">
							<view class="uni-list-cell-db">
								<picker mode="time" :value="time1" start="00:00" end="23:59" @change="bindTimeChange1">
									<view class="uni-input">{{time1?time1:'请选择'}}</view>
								</picker>
							</view>
						</view>
					</view>
					<span class="iconfont icon-weibiaoti34"></span>
				</div>
			</div>
			<div class="item flex">
				<div class="il">下车位置</div>
				<div class="ir" @click="onLocate(1)">{{locate1?locate1:'请选择'}} <span class="iconfont icon-weibiaoti34"></span></div>
			</div>
			<block v-if="type_index == 2">
				<div class="item flex">
					<div class="il">下车时间(回)</div>
					<div class="ir">
						<view class="uni-list">
							<view class="uni-list-cell">
								<view class="uni-list-cell-db">
									<picker mode="time" :value="time2" start="00:00" end="23:59" @change="bindTimeChange2">
										<view class="uni-input">{{time2?time2:'请选择'}}</view>
									</picker>
								</view>
							</view>
						</view>
					<span class="iconfont icon-weibiaoti34"></span></div>
				</div>
				<div class="item flex">
					<div class="il">下车位置</div>
					<div class="ir" @click="onLocate(2)">{{locate2?locate2:'请选择'}} <span class="iconfont icon-weibiaoti34"></span></div>
				</div>
			</block>
		</div>
		<div class="tip">备注信息</div>
		<textarea value="" placeholder="请输入备注信息" />
		<div class="button" @click="confirm">确定</div>
	</div>
</template>

<script>
	import litem from '../components/line.vue'
	export default {
		components: {
			litem,
		},
		data(){
			return {
				value:1,
				block:[
					{
						title:'总部A',
						line:['大成花园','大成花园','大成花园','大成花园','大成花园','大成花园','大成花园']
					},{
						title:'总部A',
						line:['大成花园','大成花园','大成花园','大成花园','大成花园','大成花园','大成花园']
					}
				],
				type:['去上班','下班回家','往返'],
				type_index:'',
				type_on:'',
				
				time1:'',
				time2:'',
				locate1:'',
				locate2:'',
			}
		},
		methods:{
			onType(){
				uni.showActionSheet({
					itemList:this.type,
					success:(res)=>{
						if(this.type_index != res.tapIndex){
							// 清除之前输入
							this.time1='';
							this.time2='';
							this.locate1='';
							this.locate2='';
						}
						this.type_index = res.tapIndex
						this.type_on=this.type[res.tapIndex]
					}
				})
			},
			bindTimeChange1: function(e) {
				this.time1 = e.target.value
			},
			bindTimeChange2: function(e) {
				this.time2 = e.target.value
			},
			onLocate(data){
				let that = this;
				uni.chooseLocation({
				    success: function (res) {
				        console.log('位置名称：' + res.name);
				        console.log('详细地址：' + res.address);
				        console.log('纬度：' + res.latitude);
				        console.log('经度：' + res.longitude);
						that[`locate${data}`] = res.name;
				    }
				});
			},
			confirm(){
				uni.navigateTo({
					url:'./vote_result'
				})
			}
		}
	}
</script>

<style scoped lang="scss">
	.main {
		padding: 0 30rpx 40rpx;
	}
	.tip {
		line-height: 90rpx;
	}
	.block {
		padding: 0 30rpx;
		border-radius: 12rpx;
		background: #fff;
		.line {
			height: 90rpx;
			border-bottom: 1rpx solid #eee;
			span {
				font-size: 32rpx;
			}
		}
		.tips {
			margin: 25rpx 0;
		}
		.item {
			padding: 0 18rpx;
			line-height: 60rpx;
			border-radius: 60rpx;
			background-color: #f2f2f2;
			margin: 0 20rpx 20rpx 0;
			display: inline-block;
		}
		.item.active {
			background-color: rgba(56,117,246,0.2);
			color: #3875F6;
		}
	}
	.block +.block {
		margin-top: 20rpx;
	}
	.msg {
		padding: 0 30rpx;
		border-radius: 12rpx;
		background: #fff;
		.item {
			height: 90rpx;
			.ir {
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
			text-align: right;
			color: #999;
		}
	}
	textarea {
		width: 100%;
		border-radius: 12rpx;
		background: #fff;
		height: 200rpx;
		box-sizing: border-box;
		padding: 30rpx;
		color: #999;
		font-size: 28rpx;
	}
	.button {
		width: 520rpx;
		line-height: 80rpx;
		border-radius: 80rpx;
		font-size: 32rpx;
		color: #fff;
		text-align: center;
		background-color: var(--blue);
		margin: 40rpx auto 0;
	}
	.moreMsg {
		margin-top: 20rpx;
		.title {
			line-height: 30rpx;
			padding-top: 20rpx;
		}
	}
</style>
