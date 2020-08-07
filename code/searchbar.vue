<template>
  <!-- 搜索栏 -->
	<view class="container">
    <view class="input-box" :style="{'background-color': backgroundColor}">
      <image class="icon__search" src="/static/images/icon_18_search@2x.png" mode="aspectFit"></image>
      <input :value="text" class="input-context"
				 name="keyword" :placeholder="placeholder" confirm-type="search" @input="onChange" @confirm="onConfirm"/>
        <view
				 class="cancel"
				 @click="reset"
				 :style="{ display: text.length > 0 ? 'block' : 'none' }"
				>
					<image
           class="image"
					 src="/static/images/icon_12_delete2@2x.png"
					 mode="aspectFit"
					/>
				</view>
    </view>
	</view>
</template>

<script lang="ts">
    import { Component,Vue ,Watch, Prop} from "vue-property-decorator";
    @Component({
      components: {
      }
    })
	export default class SearchBarComponents extends Vue{
    private text:string = ''
    @Prop() placeholder!: string
		@Prop({ type: String, default: '#F7F7F7' }) backgroundColor!: string
		onLoad() {
    }
    onChange (event:any) {
			this.text = event.mp.detail.value
		}
		onConfirm () {
			this.$emit('onChange', this.text, false);
    }
    initialText (text:string) {
      this.text = text
    }
		reset () {
			this.text = ''
			this.$emit('onChange', '', true);
		}
	};
</script>

<style lang="scss" scoped>
.container {
  // height: 32px;
  width: 100%;
  padding: 12upx 32upx;
  // background-color: #FFF;
  // border-bottom: .5px solid #DDDDDD;
}

.input-box {
  position: relative;
  display: flex;
  flex-direction: row;
  align-items: center;
  // background: $mtu-bg-button-l-grey;
  border-radius: 32upx;
  height: 64upx;
  padding: 12upx 20upx;
  font-size: 26upx;
  color: #4d4d4d;
}

.icon__search {
  height: 48upx;
  width: 48upx;
  margin-right: 16upx;
}
// $a: 100upx;
.input-context {
  font-size: 26upx;
  // width: calc(100% - #{$a});
  flex: 1;
}

.cancel {
  margin: 0;
  padding: 0;
  line-height: 0;
  display: none;
  // position: absolute;
  // right: 24upx;
  border: 0;
  // height: 36upx;
  width: 60upx;
  height: 100%;
  display: flex;
  align-items: center;
  text-align: right;
  z-index: 100;
  &:after {
    border: 0;
  }

  .image {
    height: 36upx;
    width: 36upx;
  }
}
</style>
