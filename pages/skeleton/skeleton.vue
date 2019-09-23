<template>
	<view class="skeleton">
		<view v-show="show">
			<skeleton></skeleton>
		</view>
		<view>
			<image class="skeleton-radius" src="../../static/logo.png" mode="widthFix" style="width: 100upx;height: 100upx;border-radius: 50%;"></image>
		</view>
		<view class="skeleton-rect">
			我是矩形
		</view>
	</view>
</template>

<script>
	import skeleton from "../../components/skeleton.vue";
	export default {
		data() {
			return {
				show: true
			}
		},
		components: {
			skeleton
		},
		onLoad: function() {
			setTimeout(() => {
				this.show = false;
			}, 2000)
		}
	}
</script>

<style>
</style>
