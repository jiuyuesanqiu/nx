<template>
	<view class="container" :style="containerStyle">
		<view v-for="(item,index) in skeletonRectLists" :key="index" :class="{chiaroscuro :loading == 'chiaroscuro'}" :style="{
					width: item.width + 'px',
					height: item.height + 'px',
					'background-color': color,
					position: 'absolute',
					left: item.left + 'px',
					top: item.top + 'px'
				}">
		</view>
		<view v-for="(item,index) in skeletonCircleLists" :key="index" :class="{chiaroscuro: loading == 'chiaroscuro'}"
		 :style="{
					width: item.width + 'px',
					height: item.height + 'px',
					'background-color': color,
					'border-radius': item.width + 'px',
					position: 'absolute',
					left: item.left + 'px',
					top: item.top + 'px'
				}">
		</view>
		<view class="spinbox" v-if="loading == 'spin'">
			<view class="spin"></view>
		</view>
		<div class="waves">
		</div>
	</view>
</template>

<script>
	export default {
		props: {
			color: {
				type: String,
				default: '#f5f5f5'
			},
			selector: {
				type: String,
				default: 'skeleton'
			},
			loading: {
				type: String,
				default: 'spin'
			}
		},
		data() {
			return {
				systemInfo: {},
				skeletonRectLists: [],
				skeletonCircleLists: []
			}
		},
		computed: {
			containerStyle() {
				return {
					width: this.systemInfo.width + 'upx',
					height: this.systemInfo.height + 'upx',
					'background-color': this.bgcolor
				}
			}
		},
		created: function() {
			//默认的首屏宽高，防止内容闪现
			const systemInfo = wx.getSystemInfoSync();
			this.systemInfo = {
				width: systemInfo.windowWidth,
				height: systemInfo.windowHeight
			}
		},
		onReady: function() {
			//绘制背景
			wx.createSelectorQuery().selectAll(`.${this.selector}`).boundingClientRect().exec((res) => {
				if (res[0].length !== 0) {
					this.systemInfo.height = res[0][0].height + res[0][0].top
				}
			});
			//绘制矩形
			this.rectHandle();
			//绘制圆形
			this.radiusHandle();
		},
		methods: {
			rectHandle() {
				//绘制不带样式的节点
				wx.createSelectorQuery().selectAll(`.${this.selector} >>> .${this.selector}-rect`).boundingClientRect().exec((res) => {
					this.skeletonRectLists = res[0]
				})
			},
			radiusHandle() {
				const that = this;
				wx.createSelectorQuery().selectAll(`.${this.selector} >>> .${this.selector}-radius`).boundingClientRect().exec((res) => {
					this.skeletonCircleLists = res[0]
				})
			}
		}
	}
</script>

<style>
	.spinbox {
		position: fixed;
		display: flex;
		justify-content: center;
		align-items: center;
		height: 100%;
		width: 100%;
		z-index: 9999
	}

	.spin {
		display: inline-block;
		width: 64upx;
		height: 64upx;
	}

	.spin:after {
		content: " ";
		display: block;
		width: 46upx;
		height: 46upx;
		margin: 1upx;
		border-radius: 50%;
		border: 5upx solid #409eff;
		border-color: #409eff transparent #409eff transparent;
		animation: spin 1.2s linear infinite;
	}

	@keyframes spin {
		0% {
			transform: rotate(0deg);
		}

		100% {
			transform: rotate(360deg);
		}
	}

	.chiaroscuro {
		width: 100%;
		height: 100%;
		background: rgb(194, 207, 214);
		animation-duration: 2s;
		animation-name: blink;
		animation-iteration-count: infinite;
	}

	@keyframes blink {
		0% {
			opacity: .4;
		}

		50% {
			opacity: 1;
		}

		100% {
			opacity: .4;
		}
	}

	@keyframes flush {
		0% {
			left: -100%;
		}

		50% {
			left: 0;
		}

		100% {
			left: 100%;
		}
	}

	.shine {
		animation: flush 2s linear infinite;
		position: absolute;
		top: 0;
		bottom: 0;
		width: 100%;
		background: linear-gradient(to left,
			rgba(255, 255, 255, 0) 0%,
			rgba(255, 255, 255, .85) 50%,
			rgba(255, 255, 255, 0) 100%)
	}
</style>
