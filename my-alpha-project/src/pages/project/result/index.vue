<template>
  <view class="result full-height" @click="jumpReport" @>
    <u-image
      class="fixed-img"
      mode="scaleToFill"
      width="100%"
      height="100%"
      src="https://zilean.vip/static/imgs/bg5.png"
    ></u-image>
    <view class="fixed-content content">
      <view class="person-info u-m-b-20">
        <view class="desc">@{{ dataSource.nickname || "XXX" }}</view>
        <view class="desc">请查收</view>
        <view class="desc">你的声音专属报告</view>
      </view>
      <view>
        <template v-for="(v, i) in lists">
          <view :key="i" class="u-flex u-row-between u-col-center u-m-b-12">
            <u-image :width="66" :height="66" :src="v.img"></u-image>
            <view class="norm u-text-center u-m-l-8 u-m-r-8">{{
              v.label
            }}</view>
            <view class="u-flex-1">
              <custom-progress :color="v.color" :percent="40" :key="i" />
            </view>
          </view>
        </template>
      </view>
    </view>
  </view>
</template>

<script>
import { mapState, mapGetters, mapMutations } from "vuex";
import customProgress from "./components/progress.vue";
export default {
  components: { customProgress },
  data() {
    return {
      dataSource: {},
      lists: [
        { label: "温暖", img: "/static/icons/温暖.png", color: "#e05a3b" },
        { label: "神秘", img: "/static/icons/神秘.png", color: "#835fa6" },
        { label: "清澈", img: "/static/icons/清澈.png", color: "#71c7cb" },
        { label: "故事感", img: "/static/icons/故事感.png", color: "#f1b92f" },
        { label: "多巴胺", img: "/static/icons/多巴胺.png", color: "#c74995" },
        { label: "能量值", img: "/static/icons/能量值.png", color: "#f3e02e" },
      ],
    };
  },
  computed: {
    ...mapState({
      soundResult: (state) => state.soundResult,
    }),
  },
  watch: {
    soundResult: {
      immediate: true,
      handler: function (next) {
        this.dataSource = next;
      },
    },
  },
  methods: {
    jumpReport() {
      uni.navigateTo({
        url: `/pages/project/report/index`,
      });
    },
  },
  onShow() {},
};
</script>

<style lang="scss" scoped>
@import "./index.scss";
</style>
