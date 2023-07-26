<template>
  <view class="progress-container">
    <view class="progress u-flex-1">
      <view
        :style="{ width: `${percent}%`, background: color }"
        class="progress-content"
      ></view>
      <u-image
        v-if="!!showIcon"
        src="/static/icons/bee.png"
        :width="66"
        :height="66"
        :style="{left:`calc(${percent}% - 33rpx)`}"
        class="progress-icon"
      />
    </view>
    <view class="percent" v-if="!showIcon">{{ percent }}%</view>
  </view>
</template>

<script>
export default {
  data() {
    return {};
  },
  props: {
    color: {
      type: String,
      default: "#19be6b",
    },
    percent: {
      type: Number,
      default: 0,
    },
    showIcon: {
      type: Boolean,
      default: false,
    },
  },
  computed: {},
  methods: {},

  onShow() {},
};
</script>

<style lang="scss" scoped>
.progress-container {
  width: 100%;
  flex: 1;
  display: flex;
  flex-direction: row;
  align-items: center;
  .progress {
    position: relative;
    height: 48rpx;
    background: transparent;
    border-radius: 24rpx;
    border: 6rpx solid #fff;
    // overflow: hidden;
    .progress-content {
      height: 100%;
      border-radius: 24rpx;
      //   border-right: 6rpx solid #fff;
    }
  }
  .progress-icon {
    position: absolute;
    bottom: 0;
  }
  .percent {
    width: 80rpx;
    font-size: 30rpx;
    font-family: 30rpx;
    text-align: center;
    color: #fff;
  }
}
</style>
