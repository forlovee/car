<template>
	<div class="main">
		<div class="form">
			<div class="input"><span>站点</span><input v-model.trim="name" type="text" placeholder="请输入站点"><div class="button" @click="login">查询</div></div>
			<!-- <div class="input"><span>目的站点</span><input v-model.trim="number" type="text" placeholder="请输入目的站点"></div> -->
			
		</div>
		<div class="result">
			<block v-for='item in list' :key="item.title">
				<div class="line">
					<litem :msg="item" :car="true" :stop="true"></litem>
				</div>
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
				fault:false,
				name:'',
				number:'',
				list:[
					{
						line:'总部A',
						origin:'林头路',
						dest:'美的总部',
						time:2,
						num:1,
						distance:2.4
					}
				]
			}
		},
		methods:{
			login(){
				if(!this.name || !this.number) return;
				console.log(this.name)
				console.log(this.number)
				this.fault = true
				this.$emit('login',true)
			}
		}
	}
</script>

<style scoped lang="scss">
	.main {
		
	}
	
	.form {
		// height: 390rpx;
		border-radius: 12rpx;
		background: #fff;
		padding: 30rpx;
		// margin-top: 45rpx;
		position: sticky;
		top: 45rpx;
		
		.tip {
			font-size: 32rpx;
			color: #222;
			line-height: 100rpx;
		}
		.input {
			font-size: 28rpx;
			color: #999;
			// margin-bottom: 30rpx;
			padding: 0 20rpx;
			background: var(--f7);
			display: flex;
			align-items: center;
		}
		.input span {
			margin-right: 30rpx;
		}
		input {
			display: inline-block;
			height: 90rpx;
			line-height: 90rpx;
			color: #222;
			font-size: 28rpx;
			flex: 1;
			padding-right: 20rpx;
		}
		.button {
			font-size: 32rpx;
			width: 160rpx;
			height: 90rpx;
			line-height: 90rpx;
			background: var(--blue);
			margin: auto;
			text-align: center;
			border-radius: 12rpx;
			color: #fff;
		}
		.msg {
			font-size: 28rpx;
			color: #EB5232;
			width: 100%;
			position: absolute;
			left: 0;
			bottom: -70rpx;
			text-align: center;
		}
	}
	.result {
		padding: 0 30rpx;
	}
	.line {
		margin-top: 20rpx;
	}
	
	
</style>
