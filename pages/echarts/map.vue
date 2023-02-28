<template>
  <view class="content">
    <uni-ec-canvas
      ref="uni-ec-canvas"
      class="uni-ec-canvas"
      id="mapChart"
      canvas-id="charts-map"
      :ec="ec"
    ></uni-ec-canvas>
  </view>
</template>
<script>
// 获取组件
import uniEcCanvas from "../../uni-ec-canvas/uni-ec-canvas.vue";
// 获取echarts 所有API
import * as echarts from "../../uni-ec-canvas/echarts";
console.log(echarts.version);
// mock数据
import geoJson from "./mapData.js";

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
      this.$refs["uni-ec-canvas"].init((canvas, width, height, dpr) => {
        // 获取组件的 canvas、width、height 后的回调函数
        // 在这里初始化图表
        const chart = echarts.init(canvas, null, {
          width: width,
          height: height,
          devicePixelRatio: dpr, // new
        });
        canvas.setChart(chart);
        // 注入地图数据
        echarts.registerMap("henan", geoJson);
        // 配置项
        const option = {
          tooltip: {
            trigger: "item",
            formatter: "{b}: {c}",
          },
          //视觉映射组件
          visualMap: {
            min: 0,
            max: 100,
            left: "left",
            top: "bottom",
            text: ["高", "低"], // 文本，默认为数值文本
            calculable: true,
          },

          series: [
            {
              type: "map",
              mapType: "henan",
              label: {
                normal: {
                  show: true,
                },
                emphasis: {
                  textStyle: {
                    color: "#fff",
                  },
                },
              },
              itemStyle: {
                normal: {
                  borderColor: "#389BB7",
                  areaColor: "#fff",
                },
                emphasis: {
                  areaColor: "#389BB7",
                  borderWidth: 0,
                },
              },
              animation: false,

              data: [
                { name: "郑州市", value: 100 },
                { name: "洛阳市", value: 10 },
                { name: "开封市", value: 20 },
                { name: "信阳市", value: 30 },
                { name: "驻马店市", value: 40 },
                { name: "南阳市", value: 41 },
                { name: "周口市", value: 15 },
                { name: "许昌市", value: 25 },
                { name: "平顶山市", value: 35 },
                { name: "新乡市", value: 35 },
                { name: "漯河市", value: 35 },
                { name: "商丘市", value: 35 },
                { name: "三门峡市", value: 35 },
                { name: "济源市", value: 35 },
                { name: "焦作市", value: 35 },
                { name: "安阳市", value: 35 },
                { name: "鹤壁市", value: 35 },
                { name: "濮阳市", value: 35 },
                { name: "开封市", value: 45 },
              ],
            },
          ],
        };
        // 配置项设置到实例中
        chart.setOption(option);
        // 注意这里一定要返回 chart 实例，否则会影响事件处理等
        return chart;
      });
      console.log("延迟加载了");
    }, 1000); // 两秒之后延迟加载
  },
};
</script>
<style lang='scss' scoped>
// 外层容器一定要设置高度，不然canvas本身没有高度
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