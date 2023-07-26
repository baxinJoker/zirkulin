<template>
  <view class="loading-container">
    <view class="full-width full-height u-rela content">
      <u-image
        class="absolote-img"
        mode="scaleToFill"
        width="100%"
        height="100%"
        src="https://zilean.vip/static/imgs/bg4.png"
      ></u-image>
      <view class="full-width u-text-center u-m-b-4 font-norm">休息一下</view>
      <view class="full-width u-text-center u-m-b-4 font-norm"
        >吃颗润喉糖吧...</view
      >
      <view class="full-width u-m-b-8 u-flex u-row-center">
        <u-image
          mode="scaleToFill"
          :width="345"
          :height="66"
          src="https://zilean.vip/static/imgs/loading.gif"
        ></u-image>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      visible: false,
    };
  },
  // props: {
  //   value: {
  //     type: Boolean,
  //     default: false,
  //   },
  // },
  // model: {
  //   prop: "value",
  //   event: "input",
  // },
  // watch: {
  //   value: function (next) {
  //     console.log(next)
  //     this.visible = next;
  //   },
  // },
  computed: {},
  methods: {},

  onShow() {},
};
</script>

<style lang="scss" scoped>
.loading-container {
  position: fixed;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  z-index: 99999;
  .absolote-img {
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    z-index: -1;
  }
  .font-norm {
    font-size: 36rpx;
    font-family: 黑体;
    color: #fff;
  }
  .content {
    padding-top: 800rpx;
  }
}
</style>
