<!--用户基本信息页面-->
<style scoped lang="scss">
.p-switch {
  position: fixed;
  right: 100px;
  top: 20px;
  margin: 30px auto 0;
  width: 200px;
  height: 40px;
  color: white;
  cursor: pointer;
  line-height: 40px;
  font-size: 20px;
  text-align: center;
  border-radius: 4px;
  background-color: #3d8ac7;
  z-index: 2;
}
.circleSmiall {
  position: absolute;
  &:nth-of-type(1) {
    top: 80px;
    left: 80px;
  }
  &:nth-of-type(2) {
    top: 60px;
    left: 60px;
  }
  &:nth-of-type(3) {
    top: 40px;
    left: 40px;
  }
  &:nth-of-type(4) {
    top: 20px;
    left: 20px;
  }
}
.p-test {
  position: relative;
  background-color: white;
  margin: 10px;
  .btn {
    margin: 30px auto 0;
    width: 200px;
    height: 40px;
    color: white;
    line-height: 40px;
    font-size: 20px;
    cursor: pointer;
    text-align: center;
    border-radius: 4px;
    background-color: #3d8ac7;
  }
  p {
    padding: 0;
    margin: 0;
  }
  .circleTitleBox {
    width: 112px;
    height: 100px;
    position: absolute;
    top: 0;
    line-height: 20px;
    text-align: right;
    vertical-align: text-top;
    top: -5px;
    padding-right: 10px;
    box-sizing: border-box;
  }
}
</style>
<template>
  <section>
    <!-- <section class="p-switch btn" @click="isDurationModel = !isDurationModel">
      {{ isDurationModel ? '动画模式' : '持续模式' }}
    </section> -->
    <section class="p-test">
      <circle-progress
        id="circle1"
        class="circleSmiall"
        :isAnimation="true"
        :isRound="true"
        :width="width - 4 * (2 * ringSpacing)"
        :radius="radius"
        :progress="progressPro[0]"
        :barColor="barColors[0]"
        :duration="duration"
        :delay="delay"
        :timeFunction="timeFunction"
        :backgroundColor="backgroundColor"
      ></circle-progress>
      <circle-progress
        id="circle2"
        ref="$circle"
        class="circleSmiall"
        :isAnimation="true"
        :isRound="true"
        :width="width - 3 * (2 * ringSpacing)"
        :radius="radius"
        :progress="progressPro[1]"
        :barColor="barColors[1]"
        :duration="duration"
        :delay="delay"
        :timeFunction="timeFunction"
        :backgroundColor="backgroundColor"
      ></circle-progress>
      <circle-progress
        id="circle3"
        class="circleSmiall"
        :isAnimation="true"
        :isRound="true"
        :width="width - 2 * (2 * ringSpacing)"
        :radius="radius"
        :progress="progressPro[2]"
        :barColor="barColors[2]"
        :duration="duration"
        :delay="delay"
        :timeFunction="timeFunction"
        :backgroundColor="backgroundColor"
      ></circle-progress>
      <circle-progress
        id="circle4"
        class="circleSmiall"
        :isAnimation="true"
        :isRound="true"
        :width="width - 1 * (2 * ringSpacing)"
        :radius="radius"
        :progress="progressPro[3]"
        :barColor="barColors[3]"
        :duration="duration"
        :delay="delay"
        :timeFunction="timeFunction"
        :backgroundColor="backgroundColor"
      ></circle-progress>
      <circle-progress
        id="circle5"
        class="circlebig"
        :isAnimation="true"
        :isRound="true"
        :width="width"
        :radius="radius"
        :progress="progressPro[4]"
        :barColor="barColors[4]"
        :duration="duration"
        :delay="delay"
        :timeFunction="timeFunction"
        :backgroundColor="backgroundColor"
      ></circle-progress>
      <div class="circleTitleBox" style="">
        <p>test</p>
        <p>test</p>
        <p>test</p>
        <p>test</p>
        <p>test</p>
      </div>
    </section>
    <!-- :class="n == option.ringNum ? 'circleBig' : 'circleSmiall'" -->
    <section class="p-test">
      <circle-progress
        v-for="n in option.ringNum"
        :id="'circle1' + n"
        :isAnimation="true"
        :isRound="true"
        :width="option.width - (option.ringNum - n) * (2 * option.ringSpacing)"
        :radius="option.radius"
        :progress="option.progressPro[n - 1] * 0.75"
        :barColor="option.barColors[n - 1]"
        :duration="option.duration"
        :timeFunction="option.timeFunction"
        :backgroundColor="option.backgroundColor"
        :style="
          n == option.ringNum
            ? 'position:relative;'
            : 'position:absolute;top:' +
              (option.ringNum - n) * option.ringSpacing +
              'px;left:' +
              (option.ringNum - n) * option.ringSpacing +
              'px;'
        "
      ></circle-progress>
      <div class="circleTitleBox" style="">
        <p v-for="item in option.titles">{{ item }}</p>
      </div>
    </section>
  </section>
</template>
<script>
import CircleProgress from "./components/circle-progress";
import CircleCollection from "./components/circleCollection";

export default {
  components: {
    CircleProgress
  },
  data() {
    return {
      isDurationModel: false, // 是否打开持续缓动模式
      isShow: true,
      progress: 70,
      delay: 20,
      barColor: "#F2AE57",
      intervalTimer: null, // 持续模式，循环计时器
      currentTime: 0, // 当前时间
      durationTime: 60, // 持续模式总时长
      radius: 8,
      ringSpacing: 20, // 环间距
      ringNum: 5, //环的个数
      width: 220,
      // 最大环宽度  直径
      radius: 8,
      //  环宽
      progressPro: [17, 17, 17, 17, 75],
      // 各个环百分比
      barColors: ["#FF82A2", "#FEDD5E", "#70D2C9", "#5FC2FA", "#5FA1F7"],
      // 各个颜色
      duration: 500,
      // 动画时长
      titles: ["测试", "测试", "测试", "测试", "测试"],
      backgroundColor: "#F1F1F1",
      timeFunction: "cubic-bezier(0.99, 0.01, 0.22, 0.94)",

      option: {
        ringSpacing: 20, // 环间距
        ringNum: 5, //环的个数
        width: 220,
        // 最大环宽度  直径
        radius: 8,
        //  环宽
        progressPro: [17, 17, 17, 17, 100],
        // 各个环百分比
        barColors: ["#FF82A2", "#FEDD5E", "#70D2C9", "#5FC2FA", "#5FA1F7"],
        // 各个颜色
        duration: 500,
        // 动画时长
        titles: ["测试", "测试", "测试", "测试", "测试"],
        backgroundColor: "#F1F1F1",
        timeFunction: "cubic-bezier(0.99, 0.01, 0.22, 0.94)"
      }
    };
  },

  watch: {
    isDurationModel() {
      clearInterval(this.intervalTimer);
      this.currentTime = 0;
    }
  },

  methods: {
    // 重置动画
    reset() {
      this.isShow = false;
      this.$nextTick(() => {
        this.isShow = true;
      });
    },

    // 开始计时
    startTime() {
      let spaceTime = 10;
      clearInterval(this.intervalTimer);
      this.currentTime = 0;
      this.intervalTimer = setInterval(() => {
        this.currentTime += spaceTime / 1000;
        if (this.currentTime >= this.durationTime) {
          clearInterval(this.intervalTimer);
        }
      }, spaceTime);
    }
  }
};
</script>
