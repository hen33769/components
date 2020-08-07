<template>
	<view>
		<uniSwiperDots :info="info"
		               :dotsStyles="dotsStyles"
		               :current="current"
		               mode="round">
			<swiper class="swiper"
			        circular="true"
			        previous-margin="44rpx"
			        next-margin="44rpx"
			        @change="change">
				<swiper-item v-for="(item,index) in info"
				             :key="index">
					<card :infoToCard="item"></card>
				</swiper-item>
			</swiper>
		</uniSwiperDots>
	</view>
</template>

<script lang="ts">
	import { Component, Vue, Watch, Prop } from "vue-property-decorator";
	import uniSwiperDots from "@/components/uni-swiper-dot.vue"
	import card from "@/components/mine/datafeedback/card.vue"
	import { card_info } from "@/utils/globalclass"
	@Component({
		components: {
			uniSwiperDots,
			card
		}
	})
	export default class banner extends Vue {
		@Prop({ type: Array, default: {} }) info!: card_info
		// private phone_number:String = ''
		private dotsStyles: object = {}
		private current: number = 0
		constructor() {
			super()
			this.dotsStyles = {
				width: "4rpx",
				border: '2rpx #DDDDDD solid',
				selectedBorder: 'none',
				backgroundColor: '#FFFFFF',
				selectedBackgroundColor: '#FFDA04'
			}
		}
		onLoad() {}
		change(event: any) {
			this.current = event.detail.current
		}
	};
</script>

<style lang="scss"
       scoped>
	.swiper {
		height: 270upx;

	}
</style>
