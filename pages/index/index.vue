<template>
	<view>
		<view v-show="show">
			<skeleton></skeleton>
		</view>
	</view>
</template>

<script>
	import skeleton from "../../components/skeleton.vue";
	export default {
		data() {
			return {
				show: false
			}
		},
		components: {
			skeleton
		},
		onLoad: function() {
		}
	}
</script>

<style>
</style>
