<template>
  <view class="recording full-height">
    <u-image
      class="fixed-img"
      mode="scaleToFill"
      width="100%"
      height="100%"
      src="https://zilean.vip/static/imgs/bg3.png"
    ></u-image>
    <view class="fixed-content content">
      <view class="content-body u-flex u-row-between">
        <u-icon
          class="u-flex-1"
          name="play-left-fill"
          color="#ebd74a"
          size="60"
        ></u-icon>
        <view class="record-content">
          <view class="record-texts">
            <view class="u-font-40 u-text-center record-text">
              内切圆外接圆</view
            >
            <view class="u-font-40 u-text-center record-text">
              祝你阖家团圆
            </view>
            <view class="u-font-40 u-text-center record-text">
              三角形四边形
            </view>
            <view class="u-font-40 u-text-center record-text">
              祝你样样都行
            </view>
          </view>
        </view>
        <u-icon
          class="u-flex-1"
          name="play-right-fill"
          color="#ebd74a"
          size="60"
        ></u-icon>
      </view>
    </view>
    <u-button
      class="recording-btn"
      type="warning"
      @longpress="longpressBtn"
      @touchend="touchendBtn"
      >{{ longPress == "1" ? "长按录音" : "录音中..." }}</u-button
    >
    <u-button class="next-btn" type="warning" @click="jumpPersonInfo"
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
          // image: "https://cdn.uviewui.com/uview/swiper/1.jpg",
          title: "昨夜星辰昨夜风，画楼西畔桂堂东",
        },
        {
          // image: "https://cdn.uviewui.com/uview/swiper/2.jpg",
          title: "身无彩凤双飞翼，心有灵犀一点通",
        },
        {
          // image: "https://cdn.uviewui.com/uview/swiper/3.jpg",
          title: "谁念西风独自凉，萧萧黄叶闭疏窗，沉思往事立残阳",
        },
      ],
      rm: null,
      timer: null,
      init: null,
      count: null, // 录制倒计时
      longPress: "1", // 1显示 按住说话 2显示 说话中
      delShow: false, // 删除提示框显示隐藏
      time: 0, //录音时长
      duration: 60000, //录音最大值ms 60000/1分钟
      tempFilePath: "", //音频路径
      playStatus: 0, //录音播放状态 0:未播放 1:正在播放
    };
  },
  computed: {},
  methods: {
    ...mapMutations(["changeParamters"]),
    jumpPersonInfo() {
      if (!this.tempFilePath) {
        uni.showToast({
          icon: "none",
          title: "请录音",
          position: "top",
        });
        return;
      }
      this.changeParamters({ tempFilePath: this.tempFilePath });
      uni.navigateTo({
        url: `/pages/project/personInfo/index`,
      });
    },
    countdown(val) {
      let _then = this;
      _then.count = Number(val);
      this.timer = setInterval(function () {
        if (_then.count > 0) {
          _then.count--;
        } else {
          _then.longPress = "1";
          clearInterval(this.timer);
        }
      }, 1000);
    },
    // 长按录音事件
    longpressBtn() {
      this.longPress = "2";
      this.countdown(60); // 倒计时
      clearInterval(this.timer); // 清除定时器
      const options = {
        duration: this.duration, // 指定录音的时长，单位 ms
        sampleRate: 16000, // 采样率
        numberOfChannels: 1, // 录音通道数
        encodeBitRate: 96000, // 编码码率
        format: "mp3", // 音频格式，有效值 aac/mp3
        frameSize: 10, // 指定帧大小，单位 KB
      };
      this.recordingTimer();
      this.rm.start(options);
      // 监听音频开始事件
      this.rm.onStart((res) => {
        console.log(res);
      });
    },
    // 长按松开录音事件
    touchendBtn() {
      this.longPress = "1";
      this.rm.onStop((res) => {
        uni.showToast({
          icon: "none",
          title: "录音成功",
          position: "top",
        });
        this.tempFilePath = res.tempFilePath;
      });
      this.recordingTimer(this.time);
      this.rm.stop();
    },
    recordingTimer(time) {
      var that = this;

      if (time == undefined) {
        // 将计时器赋值给init
        this.init = setInterval(function () {
          that.time++;
        }, 1000);
      } else {
        clearInterval(this.init);
      }
    },
  },
  mounted() {
    if (this.rm === null) {
      // 录音管理器如果没有初始化就先初始化
      this.rm = uni.getRecorderManager();
    }
    // uni.authorize({
    //   scope: "scope.record",
    //   success: function () {
    //     if (this.rm === null) {
    //       // 录音管理器如果没有初始化就先初始化
    //       this.rm = uni.getRecorderManager();
    //     }
    //   },
    //   fail(){
    //     uni.showModal({
    //       content:'检测到你没有打开录音功能权限，是否去设置打开？',
    //       confirmText:'确认',
    //       cancelText:'取消',
    //       success(res){
    //         uni.openSetting({
    //           success(r){
    //             console.log(r)
    //           },
    //           fail(r){
    //             showToast({
    //               title:'打开授权设置失败',
    //               icon:'none'
    //             })
    //           }
    //         })
    //       }
    //     })
    //   }
    // });
  },
  beforeDestroy() {
    this.rm = null;
  },
  onShow() {},
};
</script>

<style lang="scss" scoped>
@import "./index.scss";
</style>
