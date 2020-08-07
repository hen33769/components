<template>
	<view class="feedback-wrap">
		<view class="left">
			<view class="title">
				{{f_list.f_title}}
			</view>
			<view class="type">
				<image class="t-icon" :src="f_list.f_icon || '/static/images/fileicon/ppt_icon@2x.png'"></image>
				<view class="text">
					{{f_list.f_text}}
				</view>
			</view>
			<view class="visible">
				<image class="v-icon" :src="f_list.f_visible_icon || '/static/images/tabicon/icon_org_def@2x.png'"></image>
				<view class="text">
					{{f_list.f_visible_text}}
				</view>
			</view>
		</view>
		<view class="right">
			<view class="text">
				观看次数
			</view>
			<view class="r-number">
				{{f_list.show_number}}
			</view>
		</view>
	</view>
</template>

<script lang="ts">
	import { Component, Vue, Watch, Prop } from "vue-property-decorator";
	import { feedback_data } from "@/utils/globalclass"
	@Component({
		components: {}
	})
	export default class List extends Vue {
		// private phone_number:String = ''
		@Prop({ type: Object, default: {} }) f_list!: feedback_data
		onLoad() {}
	};
</script>

<style lang="scss"
       scoped>
	.feedback-wrap {
		background-color: #FFFFFF;
		width: 91.5%;
		height: 104px;
		margin: 16px auto 0;
		padding: 12px 0;
		border-radius: 8px;
		box-shadow: 0 0 8px 0 rgba($color: #3e473b, $alpha: 0.1);
		display: flex;
		justify-content: space-between;

		.text {
			font-size: 12px;
			color: #999999;
		}

		.left {
			width: calc(100% - 100px);
			border-right: 1px #F1F1F1 solid;
			padding: 0 16px;

			.title {
				// max-width: 215px;
				color: #333333;
				font-size: 16px;
				font-weight: bold;
				margin-bottom: 12px;
				overflow: hidden;
				text-overflow: ellipsis;
				white-space: nowrap;
			}

			.type {
				display: flex;
				align-items: center;

				.t-icon {
					width: 24px;
					height: 24px;
					margin-right: 4px;
				}

			}

			.visible {
				display: flex;
				margin-top: 8px;
				align-items: center;

				.v-icon {
					width: 12px;
					height: 12px;
					margin-right: 4px;
				}

			}

		}

		.right {
			flex-grow: 0;
			display: flex;
			flex-direction: column;
			justify-content: center;
			align-items: center;
			width: 100px;
			min-width: 100px;

			.r-number{
				font-size: 28px;
				color: #e95623;
				margin-top: 8px;
			}
		}

	}
</style>
