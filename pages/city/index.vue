<template>
	<div class="main">
		<top title="城际公交"></top>
		<div class="locate"></div>
	</div>
</template>

<script>
	import top from '../components/top.vue'
	export default {
		components: {
			top
		},
		data(){
			return {
				
			}
		}
	}
</script>

<style scoped lang="scss">
	page {
		padding-top: calc(44px + env(safe-area-inset-top));
	}
</style>
