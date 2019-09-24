<template>
	<view>
		<input :adjust-position="adjust" :style="{ bottom: bottom+'px' }" class="input" type="text" auto-focus placeholder="请输入" @keyboardheightchange="keyboardheightchange" />
	</view>
</template>

<script>
export default {
	props: {
		// 是否上推页面
		adjust: {
			type: Boolean,
			default: true
		}
	},
	data() {
		return {
			bottom: 0
		};
	},
	methods: {
		keyboardheightchange({ detail }) {
			if (!this.adjust) {
				this.bottom = detail.height;
			}
			if (detail.height === 0) {
				this.$emit('hide');
			}
		}
	}
};
</script>

<style lang="scss">
.input {
	position: absolute;
	bottom: 0;
}
</style>
