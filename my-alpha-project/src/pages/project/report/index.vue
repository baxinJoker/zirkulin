<template>
  <view class="home full-height">
    <u-image
      mode="widthFix"
      width="100%"
      src="https://zilean.vip/static/imgs/bg6.png"
    ></u-image>
  </view>
</template>

<script>
export default {
  data() {
    return {};
  },
  computed: {},
  methods: {
    jumpAuth() {
      uni.navigateTo({
        url: `/pages/project/auth/index`,
      });
    },
  },
  onShow() {},
};
</script>

<style lang="scss" scoped>
@import "./index.scss";
</style>
