<template>
	<div class="main">
		<div class="result">
			<block v-for='item in list' :key="item.title">
				<litem :msg="item" :shou="true"></litem>
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
					},{
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
	}
</script>

<style scoped lang="scss">
	.main {
		padding: 30rpx;
	}
</style>
