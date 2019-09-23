<template>
	<view>
		 <button @click="skeleton">骨架屏</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
			}
		},
		onLoad: function() {
		},
		methods:{
			skeleton(){
				 uni.navigateTo({
				 	url:'../skeleton/skeleton'
				 })
			}
		}
	}
</script>

<style>
</style>
