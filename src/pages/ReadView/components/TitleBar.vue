<template>
  <view
    class="nav"
    :class="{show: showHeader}"
    :style="{backgroundColor: readTheme.viewColor.backgroundColor, color: readTheme.viewColor.fontColor}"
  >
    <view class="header">{{ catalogueList[fileIndex] }}</view>
    <label
      class="iconfont nav-item"
      :style="{color: isStar ? '#b2b2b2' : ''}"
      @click="handleAddToRackClick"
    >&#xe630;</label>
    <label class="iconfont nav-item" @click="handleToCommentClick">&#xe62d;</label>
    <view class="iconfont nav-item share" @click="handleShareClick">
      &#xe624;
      <button open-type="share" />
    </view>
  </view>
</template>

<script>
import { mapState } from "vuex";
export default {
  data() {
    return {
      showHeader: false
    };
  },

  computed: {
    ...mapState(["isStar", "catalogueList", "fileIndex", "readTheme"])
  },

  methods: {
    handleAddToRackClick() {
      this.$emit("handleAddToRackClick");
    },
    handleToCommentClick() {
      this.$emit("handleToCommentClick");
    },
    handleShareClick() {
      this.$emit("handleShareClick");
    },
    handleControlTitle(scroll) {
      if (scroll) this.showHeader = false;
      else this.showHeader = !this.showHeader;
    }
  }
};
</script>

<style lang="scss" scoped>
@import "@/assets/styles/common.scss";
.nav {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  position: fixed;
  z-index: 99;
  width: 100%;
  height: 120rpx;
  padding: 0 25rpx;
  background-color: #fff;
  box-shadow: 0 2px 6px 0 rgba(0, 0, 0, 0.12);
  opacity: 0;
  transform: translateY(-120rpx);
  transition: all 0.2s ease-out;
  .header {
    width: 100%;
    font-size: 14px;
    @include ellipsis;
    color: #a0a5ab;
  }
  &.show {
    transform: translateY(0);
    opacity: 1;
  }
  .nav-item {
    margin: 0 20rpx;
    font-size: 24px;
    color: #444c57;
  }
  .share {
    position: relative;
    button {
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      opacity: 0;
    }
  }
}
</style>
