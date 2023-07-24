<template>
  <view class="personInfo full-height">
    <u-image
      class="fixed-img"
      mode="scaleToFill"
      width="100%"
      height="100%"
      src="https://zilean.vip/static/imgs/bg4.png"
    ></u-image>

    <view class="fixed-content content">
      <u-form
        :model="form"
        ref="uForm"
        label-align="right"
        label-width="auto"
        :label-style="{ color: '#fff', fontSize: '40rpx', fontFamily: '黑体' }"
      >
        <u-form-item label="昵称：" prop="nickname">
          <u-input
            v-model="form.nickname"
            :border="true"
            :placeholder="null"
            class="custom-input"
          />
        </u-form-item>
        <u-form-item label="年龄：" prop="submitAge">
          <u-input
            v-model="form.submitAge"
            :border="true"
            :placeholder="null"
            type="number"
            class="custom-input"
          />
        </u-form-item>
      </u-form>
    </view>
    <u-button class="report-btn" type="warning" @click="jumpResult"
      >生成报告</u-button
    >
  </view>
</template>

<script>
import { mapState, mapGetters, mapMutations } from "vuex";
export default {
  data() {
    return {
      uploadHeader: {},
      form: {},
      rules: {
        nickname: [{ required: true, message: "昵称为必填项！" }],
        submitAge: [{ required: true, message: "年龄为必填项！" }],
      },
    };
  },
  computed: {
    ...mapState({
      projectForm: (state) => state.projectForm,
    }),
  },
  methods: {
    ...mapMutations(["saveResult"]),
    jumpResult() {
      this.$refs.uForm.validate(async (valid) => {
        if (valid) {
          uni.uploadFile({
            url: "https://zilean.vip/zkl/submit",
            filePath: this.projectForm.tempFilePath,
            fileType: "audio",
            name: "file",
            header: this.uploadHeader,
            formData: {
              ...this.projectForm,
              ...this.form,
              submitAge: Number(this.form.submitAge),
            },
            success: (data) => {
              try {
                const res = JSON.parse(data.data);
                if (res.msg == "成功") {
                  this.saveResult({ ...res.data });
                  uni.navigateTo({
                    url: `/pages/project/result/index`,
                  });
                }
              } catch (error) {
                uni.navigateTo({
                  url: `/pages/project/result/index`,
                });
              }
            },
            fail: (err) => {
              uni.navigateTo({
                url: `/pages/project/result/index`,
              });
              console.log(err);
            },
          });
        } else {
          console.log("报告生成失败");
        }
      });
    },
  },
  mounted() {
    this.$refs.uForm.setRules(this.rules);
  },
  onShow() {},
};
</script>

<style lang="scss" scoped>
@import "./index.scss";
</style>
