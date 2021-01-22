<template>
	<div class="login">
		<div class="bg">
			<image src="../../static/login.png" mode="widthFix"></image>
		</div>
		<div class="form">
			<div class="tip">验证信息</div>
			<div class="input"><span><!-- 员工本人姓名 -->账号</span><input v-model.trim="name" type="text" ></div>
			<div class="input"><span><!-- 身份证(后6位) -->密码</span><input v-model.trim="number" type="password" ></div>
			<div class="button" @click="login">确定</div>
			<div class="msg" v-if="fault">输入密码错误，请重新输入</div>
		</div>
	</div>
</template>

<script>
	export default({
		props:['fault'],
		data(){
			return {
				name:'',
				number:''
			}
		},
		methods:{
			login(){
				if(!this.name || !this.number) return;
				this.$emit('login',{name:this.name,number:this.number})
			}
		}
	})
</script>

<style scoped lang="scss">
	input::placeholder {
	  color: red;
	}
	.login {
		height: 100%;
	}
	.bg {
		height: 580rpx;
		image {
			width: 100vw;
		}
	}
	.form {
		margin: 0 30rpx;
		height: 490rpx;
		border-radius: 20rpx;
		background: #fff;
		padding: 30rpx;
		position: relative;
		top:-240rpx;
		
		.tip {
			font-size: 32rpx;
			color: #222;
			line-height: 100rpx;
		}
		.input {
			font-size: 28rpx;
			color: #999;
			margin-bottom: 30rpx;
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
			flex:1;
		}
		.button {
			font-size: 32rpx;
			width: 520rpx;
			height: 80rpx;
			line-height: 80rpx;
			background: var(--blue);
			margin: auto;
			text-align: center;
			border-radius: 80rpx;
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
	
</style>
