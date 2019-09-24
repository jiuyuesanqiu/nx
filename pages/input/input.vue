<template>
	<view>
		<button type="primary" @click="showInput">点我切换输入框</button>
		<BaseInput v-if="show" @hide="show = false" :adjust="false"></BaseInput>
	</view>
</template>

<script>
import BaseInput from '../../components/BaseInput.vue';
export default {
	data() {
		return {
			show: false
		};
	},
	methods: {
		showInput() {
			this.show = true;
		}
	},
	components: {
		BaseInput
	}
};
</script>

<style></style>
