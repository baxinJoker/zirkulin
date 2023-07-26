<template>
  <view class="test full-height">
    <u-image
      class="fixed-img"
      mode="scaleToFill"
      width="100%"
      height="100%"
      src="https://zilean.vip/static/imgs/bg2.png"
    ></u-image>
    <view class="content fixed-content item-container">
      <template v-for="(item, index) in list">
        <view
          @click="selectOrCancleItem(item.value)"
          class="item u-text-center"
          :class="judgeSelected(item.value) ? 'selected-item' : ''"
          :key="index"
          :style="{ backgroundColor: item.color }"
        >
          {{ item.label }}
        </view>
      </template>
    </view>
    <u-button class="next-btn" type="warning" @click="jumpRecording"
      >下一步</u-button
    >
  </view>
</template>

<script>
import { mapState, mapGetters, mapMutations } from "vuex";
export default {
  data() {
    return {
      list: [
        {
          label: "当小孩（宠物）闯祸的时候",
          value: 1,
          color: "#f6f1a0",
        },
        {
          label: "唱到自己拿手的歌曲",
          value: 2,
          color: "#a2d082",
        },
        {
          label: "对方没有专心听你讲话的时候",
          value: 3,
          color: "#8cb7e2",
        },
        {
          label: "交了三遍的题还是不会做",
          value: 4,
          color: "#f19db0",
        },
        {
          label: "吵架情绪失控",
          value: 5,
          color: "#f6b972",
        },
        {
          label: "群体活动听到对方喊口号更响亮",
          value: 6,
          color: "#f29988",
        },
        {
          label: "对方无法理解你想要表达的意思",
          value: 7,
          color: "#aadad9",
        },
        {
          label: "为自己的偶像应援",
          value: 8,
          color: "#4e8dca",
        },
        {
          label: "在路上遇到熟悉的人打招呼",
          value: 9,
          color: "#b19ecb",
        },
        {
          label: "晨读背书的时候",
          value: 10,
          color: "#756ecb",
        },
      ],
      scene: [],
    };
  },
  computed: {},
  methods: {
    ...mapMutations(["changeParamters"]),
    judgeSelected(value) {
      return this.scene.includes(value);
    },
    selectOrCancleItem(value) {
      //场景选择或者反选
      if (this.scene.includes(value)) {
        this.scene = [...this.scene].filter((v) => v != value);
      } else {
        this.scene = [...this.scene, value];
      }
    },
    jumpRecording() {
      this.changeParamters({ scene: JSON.stringify([...this.scene]) });
      uni.navigateTo({
        url: `/pages/project/recording/index`,
      });
    },
  },
  onShow() {},
};
</script>

<style lang="scss" scoped>
@import "./index.scss";
</style>
