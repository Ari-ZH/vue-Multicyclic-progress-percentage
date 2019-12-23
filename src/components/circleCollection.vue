<style scoped lang="scss">
.circles {
  position: relative;
  background-color: white;
  margin: 10px;
  p {
    margin: 0;
    padding: 0;
  }
}
.circleTitleBox {
  position: absolute;
  text-align: right;
  padding-right: 10px;
  box-sizing: border-box;
}
</style>
<template>
  <!-- v-if ='isShow' -->
  <section class="circles">
    <!--  -->
    <circle-progress
      v-for="n in options.ringNum"
      :key="n+keyValue[n - 1]"
      :id="'circle1' + n"
      :isAnimation="options.isAnimation"
      :isRound="options.isRound"
      :width="options.width - (options.ringNum - n) * (2 * options.ringSpacing)"
      :radius="options.radius"
      :progress="options.progressPro[n - 1] * 0.75"
      :barColor="options.barColors[n - 1]"
      :duration="options.duration"
      :timeFunction="options.timeFunction"
      :backgroundColor="options.backgroundColor"
      :style="
        n == options.ringNum
          ? 'position:relative;'
          : 'position:absolute;top:' +
            (options.ringNum - n) * options.ringSpacing +
            'px;left:' +
            (options.ringNum - n) * options.ringSpacing +
            'px;'
      "
    ></circle-progress>
    <div
      class="circleTitleBox"
      :style="{
        width: options.width / 2 + 10 + 'px',
        height: options.width / 2 + 'px',
        top: '-' + options.ringSpacing / 2.6 + 'px',
        lineHeight: options.ringSpacing + 'px'
      }"
    >
      <div
        v-for="(item, i) in titlesr"
        style="display:flex;justify-content:space-between;"
      >
        <!-- {{
          `${item} ${options.progressPro[options.progressPro.length - i - 1]}%`
        }} -->
        <div style="text-align:right;flex-grow:1;">{{ item }}</div>
        <div style="flex-basis:32px;flex-shrink:0;">
          {{ options.progressPro[options.progressPro.length - i - 1] + "%" }}
        </div>
      </div>
    </div>
  </section>
</template>
<script>
import CircleProgress from "./circle-progress";
export default {
  created() {
    if (!this.option.width) {
      this.$set(this.option, "width", 250);
    }
    if (!this.option.radius) {
      this.$set(this.option, "radius", 8);
    }
    if (!this.option.backgroundColor) {
      this.$set(this.option, "backgroundColor", "#F1F1F1");
    }
    if (!this.option.duration) {
      this.$set(this.option, "duration", "1000");
    }
    if (!this.option.delay) {
      this.$set(this.option, "delay", "500");
    }
    // console.log(this.option.ringNum)
    let keys = new Array(this.option.ringNum)
    // console.log(keys)
    keys.fill(0)
    keys.forEach((item,index)=>{
      keys[index] = index
    })
    this.keyValue = keys;
  },
  components: {
    CircleProgress
  },
  computed: {
    titlesr() {
      return this.option.titles.reverse();
    }
  },
  props: {
    option: {
      ringNum:[Number],
      width: {
        type: [Number, String],
        default: 250
      }, // 最大圆的大小
      radius: {
        type: [Number, String],
        default: 8
      }, // 进度条厚度
      progressPro: {
        type: Array
      }, // 进度条百分比
      barColor: {
        type: Array
      }, // 进度条颜色
      backgroundColor: {
        type: String,
        default: "#F1F1F1"
      }, // 背景颜色
      isAnimation: {
        // 是否是动画效果
        type: Boolean,
        default: false
      },
      isRound: {
        // 是否是圆形画笔
        type: Boolean,
        default: false
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
  },
  data() {
    return {
      options: this.option,
      isShow: true,
      keyValue: []
    };
  },
  watch: {
    options: {
      handler() {
        // 已知两种方式刷新视图   一个是if属性的改变， 一个是key值变化 
        // 这里的reset就是if属性改变,key value就是修改key值嘛,
        // v-if修改,实测也没有引起显示上的闪烁,效果还可,但是还是用key值修改好些.
        // this.reset();
        var test = new Array()
        this.keyValue.forEach(item => {
          test.push((item+1))
        });
        this.keyValue = test
      console.log('options')

      },
      deep: true
    },
    keyValue(){
      console.log('修改keyvalue')
    }
  },
  methods: {
    reset() {
      //  console.log('reset')
      this.isShow = false;
      this.$nextTick(() => {
        this.isShow = true;
      });
    }
  }
};
</script>
