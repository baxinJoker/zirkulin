<template>
  <view class="auth full-height">
    <u-image
      class="fixed-img"
      mode="scaleToFill"
      width="100%"
      height="100%"
      src="https://zilean.vip/static/imgs/bg1.png"
    ></u-image>
    <view class="content fixed-content">
      <view class="u-flex u-row-center item-container u-m-b-48">
        <view class="item" @click="jumpTest('teacher')">
          <view class="u-text-center">我是光荣的</view>
          <view class="u-text-center">人民教师</view>
        </view>
      </view>
      <view class="u-flex u-row-between item-container">
        <view class="item" @click="jumpTest('1')">
          <view class="u-text-center">我的工作是</view>
          <view class="u-text-center">高频用嗓职业</view>
        </view>
        <view class="item" @click="jumpTest('0')">
          <view class="u-text-center">我的工作</view>
          <view class="u-text-center">并不费嗓子</view>
        </view>
      </view>
    </view>
  </view>
</template>

<script>
import { mapState, mapGetters, mapMutations } from "vuex";
export default {
  data() {
    return {};
  },
  computed: {},
  methods: {
    ...mapMutations(["changeParamters"]),
    jumpTest(mark) {
      this.changeParamters({ job: mark });
      uni.navigateTo({
        url: `/pages/project/test/index`,
      });
    },
    getUserProfile() {
      uni.getUserInfo({
        desc: "登录验证",
        success: async (userInfoRes) => {
          uni.login({
            provider: "weixin",
            success: async (res) => {
              this.code = res.code;
              if (res.errMsg == "login:ok") {
                this.sendLoginDataToServer(res.code, userInfoRes.userInfo);
              }
            },
          });
        },
        fail: () => {
          uni.showToast({
            title: "授权已取消",
            icon: "error",
            mask: true,
          });
        },
      });
    },
    sendLoginDataToServer(code, userInfo) {
      // 在这里将 code 和 userInfo 发送给后台服务器
      // 后台服务器处理登录过程，返回登录态给小程序
      console.log(code, userInfo);
    },
  },
  onShow() {},
  mounted() {
    this.getUserProfile();
  },
};
</script>

<style lang="scss" scoped>
@import "./index.scss";
</style>
