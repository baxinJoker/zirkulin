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
      <view class="person-info u-m-b-30">
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
              <custom-progress
                :color="v.color"
                :percent="calcProp(v.prop)"
                :key="i"
              />
            </view>
          </view>
        </template>
      </view>
      <view class="result-age">您的声音年龄是：{{ outAge }}</view>
      <view class="result-grade">您的声音疲惫指数：{{ fatigueGrade }}</view>
      <view class="result-percent">
        <custom-progress color="#e05a3b" :percent="percent" :showIcon="true" />
      </view>
      <view class="result-text-percent u-text-center"
        >您的声音疲惫指数高于{{ percent }}%的用户</view
      >
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
        {
          label: "温暖",
          img: "/static/icons/温暖.png",
          color: "#e05a3b",
          prop: "warm",
        },
        {
          label: "神秘",
          img: "/static/icons/神秘.png",
          color: "#835fa6",
          prop: "mysterious",
        },
        {
          label: "清澈",
          img: "/static/icons/清澈.png",
          color: "#71c7cb",
          prop: "clear",
        },
        {
          label: "故事感",
          img: "/static/icons/故事感.png",
          color: "#f1b92f",
          prop: "storySense",
        },
        {
          label: "多巴胺",
          img: "/static/icons/多巴胺.png",
          color: "#c74995",
          prop: "dopamine",
        },
        {
          label: "能量值",
          img: "/static/icons/能量值.png",
          color: "#f3e02e",
          prop: "energyValue",
        },
      ],
    };
  },
  computed: {
    ...mapState({
      soundResult: (state) => state.soundResult,
    }),
    outAge() {
      return this.dataSource.outAge || 50;
    },
    fatigueGrade() {
      return this.dataSource.fatigueGrade || 5;
    },
    percent() {
      let value = Number(this.dataSource.percent || 0);
      let valueString = value.toString();
      let dotaftervalue = valueString.split(".")[1];
      if (dotaftervalue) {
        let dotlen = dotaftervalue.length;
        console.log(dotaftervalue, dotlen);
        return (Number(dotaftervalue) * Math.pow(10, 2)) / Math.pow(10, dotlen);
      } else {
        return 0;
      }
    },
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
    calcProp(prop) {
      // return (
      //   this.dataSource &&
      //   this.dataSource.extParams &&
      //   Number(this.dataSource.extParams[prop] || 0).toFixed(2) * 100
      // );

      let value =
        (this.dataSource &&
          this.dataSource.extParams &&
          Number(this.dataSource.extParams[prop] || 0)) ||
        0;
      let valueString = value.toString();
      let dotaftervalue = valueString.split(".")[1];
      if (dotaftervalue) {
        let dotlen = dotaftervalue.length;
        console.log(dotaftervalue, dotlen);
        return (Number(dotaftervalue) * Math.pow(10, 2)) / Math.pow(10, dotlen);
      } else {
        return 0;
      }
    },
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
