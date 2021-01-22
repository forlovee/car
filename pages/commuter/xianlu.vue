<template>
	<div class="main">
		<div class="form flex">
			<div class="input flex"><span class="iconfont icon-sousuo"></span><input v-model.trim="number" type="text" placeholder="搜索目的地,线路名"></div>
			<div class="button" @click="login">搜索</div>
		</div>
		<div class="result">
			<block v-for='(item,index) in list' :key="item.title">
				<litem :msg="item" :index="index" :star="true" @collect="collect"></litem>
			</block>
		</div>
		<div class="bottom">我是有底线的</div>
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
				fault:false,
				name:'',
				number:'',
				list:[
					{
						id:1,
						line:'总部A',
						dest:'美的总部',
						time:2,
						num:1,
						distance:2.4,
						status:null
					}
				]
			}
		},
		methods:{
			collect(data){
				// console.log(data)
				this.list[data.index].status = !this.list[data.index].status;
			}
		}
	}
</script>

<style scoped lang="scss">
	.main {
		padding: 0 30rpx;
	}
	.form {
		margin: 30rpx 0;
		height: 90rpx;
		border-radius: 90rpx;
		background: #eee;
		padding: 0 10rpx 0 30rpx;
		.input,input {
			flex: 1;
			font-size: 28rpx;
		}
		input {
			padding: 0 15rpx;
		}
		.button {
			width: 120rpx;
			text-align: center;
			height: 80rpx;
			line-height: 80rpx;
			border-radius: 80rpx;
			background: var(--blue);
			color: #fff;
		}
	}
	
	.result {
		/deep/ .litem:last-child .item {
			border: none;
		}
	}
	
	.bottom {
		margin: 30rpx 0;
		color: #999;
		text-align: center;
	}
</style>
