<!--用户基本信息页面-->
<style scoped lang="scss">
// .p-switch {
//   position: fixed;
//   right: 100px;
//   top: 20px;
//   margin: 30px auto 0;
//   width: 200px;
//   height: 40px;
//   color: white;
//   cursor: pointer;
//   line-height: 40px;
//   font-size: 20px;
//   text-align: center;
//   border-radius: 4px;
//   background-color: #3d8ac7;
//   z-index: 2;
// }
// .circleSmiall {
//   position: absolute;
//   &:nth-of-type(1) {
//     top: 80px;
//     left: 80px;
//   }
//   &:nth-of-type(2) {
//     top: 60px;
//     left: 60px;
//   }
//   &:nth-of-type(3) {
//     top: 40px;
//     left: 40px;
//   }
//   &:nth-of-type(4) {
//     top: 20px;
//     left: 20px;
//   }
// }
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
    position: absolute;
    text-align: right;
    padding-right: 10px;
    box-sizing: border-box;
  }
}
</style>
<template>
  <section>
    <Circle-collection :option="options"></Circle-collection>
  </section>
</template>
<script>
import CircleCollection from "./components/circleCollection";

export default {
  components: {
    CircleCollection
  },
  data() {
    return {
      options: {
        ringSpacing: 30, // 环间距
        ringNum: 5, //环的个数
        width: 320,
        // 最大环宽度  直径
        radius: 10,
        //  环宽
        progressPro: [7, 17, 17, 77, 77],
        // 各个环百分比
        barColors: ["#FF82A2", "#FEDD5E", "#70D2C9", "#5FC2FA", "#5FA1F7"],
        // 各个颜色
        duration: 1000,
        // 动画时长
        titles: ["测试1", "测试2", "测试3", "测试4", "测试5"],
        backgroundColor: "#F1F1F1",
        // 动画类型
        timeFunction: "cubic-bezier(0.99, 0.01, 0.22, 0.94)",
        // isAnimation:false,
        // isRound:false
      }
    };
  },
  watch: {
  },
  methods: {
  }
};
</script>
