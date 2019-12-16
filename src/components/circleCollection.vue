<style scoped lang="scss">
.p-test {
 position: relative;
 background-color: white;
 margin: 10px;
 p{
	 margin: 0;
	 padding: 0;
 }
}
</style>
<template>
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
</template>
<script>
import CircleProgress from "./circle-progress";
export default {
  components: {
    CircleProgress
  },
  props: {
    width: {
      type: [Number, String],
      default: 250
    }, // 圆的大小
    radius: {
      type: [Number, String],
      default: 8
    }, // 进度条厚度
    progress: [Number, String], // 进度条百分比
    barColor: String, // 进度条颜色
    backgroundColor: String, // 背景颜色
    isAnimation: {
      // 是否是动画效果
      type: Boolean,
      default: true
    },
    isRound: {
      // 是否是圆形画笔
      type: Boolean,
      default: true
    },
    id: {
      // 组件的id，多组件共存时使用
      type: [String, Number],
      default: 1
    },
    duration: {
      // 整个动画时长
      type: [String, Number],
      default: 1000
    },
    delay: {
      // 延迟多久执行
      type: [String, Number],
      default: 200
    }
  }
};
</script>
