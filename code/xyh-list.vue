<template>
	<view>
		<view class='item'
		      :style="{'height': height}"
		      @click="listTap">
			<image class="logo"
			       :style="{'border-radius': list_type === file ? '' : '50%'}"
			       :src="item.icon || '/static/images/organization/icon_40_user-round@2x.png'"></image>
			<view class="right"
			      v-if="list_type === 'member'">
				<view class="member-name">
					{{item.name}}
				</view>
			</view>
			<view class="right"
			      v-else>
				<view class="row">
					<view class="title">
						{{ item.name }}
					</view>
					<image class="is-new"
					       v-if="item.is_new && list_type === 'notification'"
					       src="/static/images/mine/notification/new_icon@2x.png"></image>
					<view class="upload-time"
					      v-if="list_type === 'file'">
						{{item.show_time}}
					</view>
				</view>
				<view class="row">
					<view class="digest"
					      :style="{'display': list_type === 'audit' ? '' : 'flex'}">
						{{ item.show_info || item.validation_msg}}
						<view class="user-name"
						      v-if="list_type === 'file' && notName === false">
							<view style="margin: 0 4rpx 0 16rpx; color: #999999;">来自</view>
							{{item.username}}
						</view>
					</view>
					<view class="latest"
					      v-if="list_type === 'notification'">
						{{item.show_time}}
					</view>
				</view>
			</view>
			<view class="audit"
			      v-if="list_type === 'audit'">
				<view v-if="item.status === 1"
				      class="new">
					<view class="auditBtn"
					      @click.stop="auditClick">
						通过
					</view>
				</view>
				<view v-else
				      class="old">
					{{item.status === 2 ? '已通过' : '已拒绝'}}
				</view>
			</view>
		</view>
	</view>
</template>

<script lang="ts">
	import { Component, Vue, Watch, Prop } from "vue-property-decorator";
	import { fileInfo, type_item } from "@/utils/globalclass"
	@Component({
		components: {}
	})
	export default class XYHList extends Vue {
		// private phone_number:String = ''
		@Prop({ type: Object, default: {} }) item!: fileInfo
		@Prop({ type: String, default: '' }) list_type!: string
		@Prop({ type: String, default: '' }) height!: ''
		@Prop({ type: Boolean, default: false }) notName?: boolean

		private type: object = {}
		private id: number = -1

		constructor() {
			super()
		}
		onLoad() {}
		auditClick() {
			this.$emit('auditClick')
		}
		listTap() {
			if (this.list_type === 'audit') {
				if (this.item.user_id) {
					this.id = this.item.user_id
					this.$emit('listTap', this.id)
				} else {
					this.$emit('listTap')
				}
			} else {
				if (this.item.file_id) {
					// this.id = this.item.file_id
					// let type: number = Number(this.item.type)
					// let upload_type: number = Number(this.item.upload_type)
					// console.log(this.id)
					// console.log(type)
					// console.log(upload_type), this.id, type, upload_type
					this.$emit('listTap')
				} else {
					this.$emit('listTap')
				}
			}
		}
	};
</script>

<style lang="scss"
       scoped>
	.item {
		width: 100%;
		display: flex;
		align-items: center;

		.logo {
			width: 80upx;
			height: 80upx;
			margin-right: 4upx;
		}


		.right {

			flex: 1;
			height: 80upx;
			padding: 6upx 24upx;
			margin-right: 4upx;
			color: #979797;
			font-size: 24upx;
			display: flex;
			flex-direction: column;
			justify-content: space-between;

			.member-name {
				color: #111111;
				font-size: 32upx;
				height: 100%;
				max-width: 440upx;
				display: flex;
				justify-content: left;
				align-items: center;
				overflow: hidden;
				text-overflow: ellipsis;
				white-space: nowrap;
			}

			.row {
				display: flex;
				justify-content: space-between;

				.title {
					color: #333333;
					font-size: 28upx;
					font-weight: Regular;
				}

				.is-new {
					width: 64upx;
					height: 32upx;
				}

				.upload-time {
					font-size: 24upx;
					color: #999999;
				}
			}

			.digest {
				max-width: 400upx;
				overflow: hidden;
				text-overflow: ellipsis;
				white-space: nowrap;

				.user-name {
					color: #62C43D;
					display: flex;
				}
			}
		}

		.audit {
			display: flex;
			justify-content: center;
			align-items: center;
			padding: 0 32upx;
			width: 184upx;

			.auditBtn {
				background-color: #63C33E;
				width: 120upx;
				height: 56upx;
				border-radius: 32upx;
				display: flex;
				align-items: center;
				justify-content: center;
				font-size: 28upx;
				line-height: 28upx;
				color: #FFFFFF;
			}
		}
	}
</style>
