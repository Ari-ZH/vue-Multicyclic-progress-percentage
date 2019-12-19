<style scoped lang="scss">
.p-test {
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
  <section class="p-test">
    <circle-progress
      v-for="n in option.ringNum"
      :key="n"
      :id="'id' + n"
      :isAnimation="option.isAnimation"
      :isRound="option.isRound"
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
    <div
      class="circleTitleBox"
      :style="{
        width: option.width / 2 + 'px',
        height: option.width / 2 + 'px',
        top: '-' + option.ringSpacing / 2.5 + 'px',
        lineHeight: option.ringSpacing + 'px'
      }"
    >
     <div v-for="(item, i) in titlesr" style="display:flex;justify-content:space-between;">
        <!-- {{
          `${item} ${option.progressPro[option.progressPro.length - i - 1]}%`
        }} -->
        <div style="text-align:right;flex-grow:1;">{{item}}</div>
        <div style="flex-basis:40px;flex-shrink:0;">{{option.progressPro[option.progressPro.length - i - 1]+'%'}}</div>
      </div>
    </div>
  </section>
</template>
<script>
import CircleProgress from "./circle-progress";
export default {
  created(){
	  if(!this.option.width){
		  this.$set(this.option, 'width', 250)
	  }
    if(!this.option.radius){
		  this.$set(this.option, 'radius', 8)
	  }
    if(!this.option.backgroundColor){
		  this.$set(this.option, 'backgroundColor',  "#F1F1F1")
    }
    if(!this.option.duration){
		  this.$set(this.option, 'duration',  "1000")
    }
    if(!this.option.delay){
		  this.$set(this.option, 'delay',  "500")
    }
  },
  components: {
    CircleProgress
  },
  computed:{
    titlesr(){
      return this.option.titles.reverse()
    }
  },
  props: {
    id:{
      type:String,
      default:'Circle'
    },
    option: {
      // 此部分以下设置无效，仅仅作为编码提示
      width: {
        type: [Number, String]
      }, // 最大圆的大小
      radius: {
        type: [Number, String]
      }, // 进度条厚度
      progress: {
        type: Array
      }, // 进度条百分比
      barColor: {
        type: Array
      }, // 进度条颜色
      backgroundColor: {
        type: String,
      }, // 背景颜色
      isAnimation: {
        // 是否是动画效果
        type: Boolean,
      },
      isRound: {
        // 是否是圆形画笔
        type: Boolean,
      },
      duration: {
        // 整个动画时长
        type: [String, Number],
      },
      delay: {
        // 延迟多久执行
        type: [String, Number],
      }
    }
  }
};
</script>
