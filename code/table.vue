<template>
	<view class="table">
		<view class="t-table">
			<view class="t-tr"
			      v-if="isTitle"
			      :style="{'height': tHeight + 'rpx', 'font-size': tFontSize + 'rpx', 'font-weight': tFontWeight, 'color': tColor, 'backgroundColor': titleBackgroundColor}">
				<view class="t-th"
				      v-for="(title, index) in titles"
				      :key="index"
				      :style="{'width': cellWidth[index] + 'rpx', 'justify-content': align, 'border-width': border + 'rpx', 'border-color': borderColor, 'padding': padding, 'font-weight': titleFontWeight}">
					<view>
						{{title.title}}
					</view>
				</view>
			</view>
			<view class="t-tr"
			      v-for="(user, index) in users"
			      :key="index"
			      :style="{'background-color': index % 2 === 0 ? backgroundColor1 : backgroundColor2, 'height': lineHeight + 'rpx', 'font-size': fontSize + 'rpx', 'font-weight': fontWeight, 'color': color}">
				<view class="t-td"
				      v-for="(data, tdIndex) in titles"
				      :key="tdIndex"
				      :style="{'width': cellWidth[tdIndex] + 'rpx', 'justify-content': align, 'border-width': border + 'rpx', 'border-color': borderColor, 'padding': padding}">
					<view class="text">
						{{user[titles[tdIndex].key]}}
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script lang="ts">
	import { Component, Vue, Watch, Prop } from "vue-property-decorator";
	import { feedback_users } from "@/utils/globalclass"
	@Component({
		components: {}
	})
	export default class Table extends Vue {
		// private phone_number:String = ''
		@Prop({ type: Array, default: {} }) users!: Array < feedback_users >
			@Prop({ type: Array, default: [] }) titles!: Array < string >
			@Prop({ type: String, default: '' }) columnWidth!: string

		@Prop({ type: Boolean, default: false }) isTitle!: boolean
		@Prop({ type: String, default: '2' }) border!: string
		@Prop({ type: String, default: 'black' }) borderColor!: string
		@Prop({ type: String, default: '0' }) padding!: string
		@Prop({ type: String, default: 'center' }) align!: string
		@Prop({ type: String, default: '' }) titleHeight!: string
		@Prop({ type: String, default: '' }) titleFontSize!: string
		@Prop({ type: String, default: '' }) titleFontWeight!: string
		@Prop({ type: String, default: '' }) titleColor!: string
		@Prop({ type: String, default: '#FFFFFF' }) titleBackgroundColor!: string
		@Prop({ type: String, default: '#F5F8F4' }) backgroundColor1!: string
		@Prop({ type: String, default: '#FFFFFF' }) backgroundColor2!: string
		@Prop({ type: String, default: '30' }) lineHeight!: string
		@Prop({ type: String, default: '30' }) fontSize!: string
		@Prop({ type: String, default: 'normal' }) fontWeight!: string
		@Prop({ type: String, default: 'black' }) color!: string

		private styles: object = {}
		private tHeight: string = this.lineHeight
		private tFontSize: string = this.fontSize
		private tFontWeight: string = this.fontWeight
		private tColor: string = this.color
		private cellWidth: Array < string > = []


		constructor() {
			super()
			this.cellWidth = this.columnWidth.split(' ')
			console.log(this.cellWidth)
		}
		onLoad() {}
	};
</script>

<style lang="scss"
       scoped>
	.table {
		.t-table {
			.t-tr {
				display: flex;

				.t-th {
					height: 100%;
					display: flex;
					align-items: center;
					border: 2upx black solid;
				}

				.t-td {
					height: 100%;
					display: flex;
					align-items: center;
					border: 2upx black solid;

					.text {
						width: 100%;
						overflow: hidden;
						text-overflow: ellipsis;
						white-space: nowrap;
					}
				}
			}
		}
	}
</style>
