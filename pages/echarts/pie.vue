<template>
  <view class="content">
    <uni-ec-canvas
      ref="uni-ec-canvas"
      class="uni-ec-canvas"
      id="mapChart"
      canvas-id="charts-pie"
      :ec="ec"
    ></uni-ec-canvas>
  </view>
</template>
<script>
// 获取组件
import uniEcCanvas from "../../uni-ec-canvas/uni-ec-canvas.vue";
// 获取echarts 所有API
import * as echarts from "../../uni-ec-canvas/echarts";

export default {
  data() {
    return {
      ec: {
        lazyLoad: true, // 延迟加载
      },
    };
  },
  components: {
    uniEcCanvas,
  },

  onLoad() {
    setTimeout(() => {
      console.log('this.$refs["uni-ec-canvas"]: ', this.$refs["uni-ec-canvas"]);
      console.log("echarts: ", echarts);
      this.$refs["uni-ec-canvas"].init((canvas, width, height, dpr) => {
        // 初始化
        const chart = echarts.init(canvas, null, {
          width: width,
          height: height,
          devicePixelRatio: dpr, // new
        });
        canvas.setChart(chart);

        // 配置项
        const option = {
          title: {
            text: "Referer of a Website",
            subtext: "Fake Data",
            left: "center",
          },
          //   提示框组件
          tooltip: {
            trigger: "item",
          },
          //   图例组件
          legend: {
            orient: "vertical",
            left: "left",
          },
          // 系列
          series: [
            {
              name: "Access From",
              type: "pie",
              radius: "50%",
              data: [
                { value: 1048, name: "Search Engine" },
                { value: 735, name: "Direct" },
                { value: 580, name: "Email" },
                { value: 484, name: "Union Ads" },
                { value: 300, name: "Video Ads" },
              ],
              emphasis: {
                itemStyle: {
                  shadowBlur: 10,
                  shadowOffsetX: 0,
                  shadowColor: "rgba(0, 0, 0, 0.5)",
                },
              },
            },
          ],
        };
        // 配置项设置到实例中
        chart.setOption(option);
        return chart;
      });
      console.log("延迟加载了");
    }, 1000); // 两秒之后延迟加载
  },
  methods: {},
};
</script>
<style lang='scss' scoped>
.content {
  width: 100%;
  height: 100vh;
}
.uni-ec-canvas {
  width: 100%;
  height: 100%;
  display: block;
}
</style>