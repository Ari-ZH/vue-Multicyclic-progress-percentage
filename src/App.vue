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
.circleSmiall{
  position: absolute;
  &:nth-of-type(1){
    top: 80px;
    left: 80px;
  }
  &:nth-of-type(2){
    top: 60px;
    left: 60px;
  }
  &:nth-of-type(3){
    top: 40px;
    left: 40px;
  }
  &:nth-of-type(4){
    top: 20px;
    left: 20px;
  }
}
.p-test {
  position: relative;
  background-color: white; 
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
  p{
    padding: 0;
    margin: 0;
  }
  .circleTitleBox{
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
    <section class="p-switch btn" @click="isDurationModel = !isDurationModel">
      {{ isDurationModel ? '动画模式' : '持续模式' }}
    </section>
    <section class="p-test" v-if="!isDurationModel">
      <circle-progress
        id = "circle1"
        v-if="isShow"
        class="circleSmiall"
        :isAnimation="true"
        :isRound="true"
        :width="60"
        :radius="8"
        :progress="'10'"
        :barColor="'#FF82A2'"
        :duration="duration"
        :delay="delay"
        :timeFunction="timeFunction"
        :backgroundColor="backgroundColor"
      ></circle-progress>
      <circle-progress
        id = "circle2"
        v-if="isShow"
        ref="$circle"
        class="circleSmiall"
        :isAnimation="true"
        :isRound="true"
        :width="100"
        :radius="8"
        :progress="'20'"
        :barColor="'#FEDD5E'"
        :duration="duration"
        :delay="delay"
        :timeFunction="timeFunction"
        :backgroundColor="backgroundColor"
      ></circle-progress>
      <circle-progress
        id='circle3'
        class="circleSmiall"
        :isAnimation="true"
        :isRound="true"
        :width="140"
        :radius="8"
        :progress="'30'"
        :barColor="'#70D2C9'"
        :duration="duration"
        :delay="delay"
        :timeFunction="timeFunction"
        :backgroundColor="backgroundColor"
      ></circle-progress>
      <circle-progress
        id='circle4'
        class="circleSmiall"
        :isAnimation="true"
        :isRound="true"
        :width="180"
        :radius="8"
        :progress="'20'"
        :barColor="'#5FC2FA'"
        :duration="duration"
        :delay="delay"
        :timeFunction="timeFunction"
        :backgroundColor="backgroundColor"
      ></circle-progress>
      <circle-progress
        id='circle5'
        class="circlebig"
        :isAnimation="true"
        :isRound="true"
        :width="220"
        :radius="8"
        :progress="'20'"
        :barColor="'#5FA1F7'"
        :duration="duration"
        :delay="delay"
        :timeFunction="timeFunction"
        :backgroundColor="backgroundColor"
      ></circle-progress>
      <div class="circleTitleBox" style=""><p>test</p><p>test</p><p>test</p><p>test</p><p>test</p></div>
    </section>
    <section class="p-test p-duration-model" v-else>
      <circle-progress
        v-if="isShow"
        ref="$circle"
        class="progress"
        key="duration-model"
        :isAnimation="false"
        :isRound="true"
        :width="width"
        :radius="radius"
        :progress="(currentTime / durationTime) * 100"
        :barColor="barColor"
        :duration="duration"
        :delay="delay"
        :timeFunction="timeFunction"
        :backgroundColor="backgroundColor"
      ></circle-progress>
      
      <ul>
        <li>
          <label for="width">圆宽（px）:</label>
          <input v-model="width" type="number" placeholder="例如：140" />
        </li>
        <li>
          <label for="radius">进度条宽度（px）:</label>
          <input v-model="radius" type="number" placeholder="例如：12" />
        </li>
        <li>
          <label for="barColor">进度条颜色:</label>
          <input v-model="barColor" type="text" placeholder="例如：#f5a623" />
        </li>
        <li>
          <label for="backgroundColor">背景颜色:</label>
          <input v-model="backgroundColor" type="text" placeholder="例如：#FFE8CC" />
        </li>
        <li>
          <label for="duration">总时长（s）:</label>
          <input v-model="durationTime" type="number" placeholder="例如：1000" />
        </li>
        <li>
          <label for="duration">当前时长（s）:</label>
          <input
            v-model="currentTime.toFixed(2)"
            type="number"
            style="color: #aaaaaa;border-color: #aaaaaa"
            disabled
            placeholder="例如：1000"
          />
        </li>
        <li>
          <div class="btn" @click="startTime">{{ currentTime > 0 ? '重新计时' : '开始计时' }}</div>
        </li>
      </ul>
    </section>
  </section>
</template>
<script>
import CircleProgress from './components/circle-progress';

export default {
  components: {
    CircleProgress
  },
  data() {
    return {
      isDurationModel: false, // 是否打开持续缓动模式
      isShow: true,
      width: 200,
      radius: 20,
      progress: 70,
      duration: 1000,
      delay: 20,
      barColor: '#F2AE57',
      backgroundColor: '#F1F1F1',
      timeFunction: 'cubic-bezier(0.99, 0.01, 0.22, 0.94)',
      intervalTimer: null, // 持续模式，循环计时器
      currentTime: 0, // 当前时间
      durationTime: 60 // 持续模式总时长
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
