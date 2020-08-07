<template>
	<view>
		<view class="item"
		      v-if="card[0]"
		      :style="{background: 'url('+card[0].background+');background-size: 100% 100%'}">
			<view class="container">
				<view class="left"
				      :style="{ 'font-size' : fontSize + 'rpx'}">
					{{show_number}}
				</view>
				<view>
					<view class="right">
						<view class="total">
							{{card[0].uptext}}
						</view>
						<view class="change">
							{{card[0].downtext}}{{card[0].change}}
						</view>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script lang="ts">
	import { Component, Vue, Watch, Prop } from "vue-property-decorator";
	import { card_info } from "@/utils/globalclass"
	@Component({
		components: {}
	})
	export default class card extends Vue {
		@Prop({ type: Object, default: {} }) infoToCard!: card_info
		// private phone_number:String = ''
		private card: Array < card_info > = []
		private changer: string = ''
		private fontSize: number = 112
		private show_number: string = ''
		constructor() {
			super()
			this.card.push(this.infoToCard)
			const query = uni.createSelectorQuery().in(this)
			let text: any = query.select('.left')
			let num: number = text._component.card[0].number
			if (num > 99999) {
				this.show_number = '99999+'
			} else {
				this.show_number = num + ''
			}
			switch (this.show_number.length) {
				case 5:
					this.fontSize = 90
					break
				case 6:
					this.fontSize = 72
					break
				default:
					this.fontSize = 112
					break
			}
		}
		onLoad() {}
	};
</script>

<style lang="scss"
       scoped>
	.item {
		height: 200upx;
		width: 640upx;
		margin: auto;

		.container {
			color: #FFFFFF;
			height: 100%;
			width: 100%;
			display: flex;
			align-items: center;

			.left {
				width: 320upx;
				text-align: right;
				padding-right: 20upx;
				padding-left: 40upx;
			}

			.right {
				width: 320upx;
				color: rgba($color: #FFFFFF, $alpha: 0.89);
				padding-left: 20upx;

				.total {
					font-size: 36upx;
					margin-bottom: 12upx;
				}

				.change {
					margin-top: 12upx;
					font-size: 28upx;
				}
			}
		}


	}
</style>
