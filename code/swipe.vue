<template>
	<view>
		<view class="news-list">
			<uni-swipe-action>
				<view class="border">
					<uni-swipe-action-item style="width: 120rpx;"
            v-for="(item, index) in list"
			      :key="index"
					  :options="options" @click="onClick($event, index)">
						<xyhList style="width: 100%;"
										 :notName="notName"
						         :item="item"
						         :height="height"
						         :list_type="list_type"
						         :check_selection="check_selection"
						         @listTap="listTap(index, item.file_id,item.type,item.upload_type,item.public_id)"
										 @auditClick="auditClick(index)"></xyhList>
					</uni-swipe-action-item>
				</view>
			</uni-swipe-action>
		</view>
	</view>
</template>

<script lang="ts">
	import { Component, Vue, Watch, Prop } from "vue-property-decorator";
	import { fileInfo } from "@/utils/globalclass"
	import uniSwipeAction from "@/components/mine/notification/uni-swipe-action.vue"
	import uniSwipeActionItem from "@/components/mine/notification/uni-swipe-action-item.vue"
	import xyhList from "@/components/xyh-list.vue"
	@Component({
		components: {
			uniSwipeAction,
			uniSwipeActionItem,
			xyhList
		}
	})
	export default class Swipe extends Vue {
		// private phone_number:String = ''
		@Prop({ type: Array, default: [] }) list!: Array < fileInfo >
		@Prop({ type: String, default: '' }) swipe_options!: string
		@Prop({ type: String, default: '' }) list_type!: string
		@Prop({ type: String, default: '' }) height!: ''
		@Prop({ type: Boolean, default: false }) check_selection!: boolean
		@Prop({ type: Boolean, default: false }) notName?: boolean
		private options: Array < object > = []

		constructor() {
			super()
			if (this.swipe_options === '删除') {
				this.options = [{
					text: '删除',
					style: {
						backgroundColor: '#F31212'
					}
				}]
			} else if (this.swipe_options === '删除+恢复') {
				this.options = [{
					text: '恢复',
					style: {
						backgroundColor: '#62C43D'
					}
				}, {
					text: '彻底删除',
					style: {
						backgroundColor: '#F31212'
					}
				}]
			} else if(this.swipe_options === '取消管理员+删除') {
				this.options = [{
					text: '取消管理员',
					style: {
						backgroundColor: '#BDC6C1'
					}
				}, {
					text: '删除',
					style: {
						backgroundColor: '#F31212'
					}
				}]
			} else if(this.swipe_options === '设为管理员+删除') {
				this.options = [{
					text: '设为管理员',
					style: {
						backgroundColor: '#62C43D'
					}
				}, {
					text: '删除',
					style: {
						backgroundColor: '#F31212'
					}
				}]
			}
		}
    onLoad() {}
    onClick (e:any, index:number) {
      this.$emit('action',index,e.index)
    }
		auditClick(index:number) {
			this.$emit('auditClick', index)
		}
		listTap(index: number, id?: number, type?: number, upload_type?: number, public_id?: number) {
			this.$emit('listTap', index, id, type, upload_type, public_id)
		}
	};
</script>

<style lang="scss"
       scoped>
	.news-list {
		background-color: #FFFFFF;

		.border {
			width: calc(100% - 32upx);
			margin-left: 32upx;
			border-bottom: 2upx #F1F1F1 solid;
		}
	}
</style>
