<template>
  <el-container>
    <el-main>
      <el-card id="card1" class="box-card">
        <draggable>
          <v-chart
            :style="{ height: height + '%', width: width + '%' }"
            :option="option"
          />
          <v-chart
            :style="{ height: height + '%', width: width + '%' }"
            :option="option"
          />
          <v-chart
            :style="{ height: height + '%', width: width + '%' }"
            :option="option"
          />
          <v-chart
            :style="{ height: height + '%', width: width + '%' }"
            :option="option"
          />
        </draggable>
      </el-card>
      <el-card id="card2" class="box-card"> </el-card>
      <el-card id="card3" class="box-card"> </el-card>
      <el-card id="card4" class="box-card"> </el-card>
    </el-main>
    <el-aside> </el-aside>
  </el-container>
</template>

<script>
import { THEME_KEY } from "vue-echarts";
export default {
  name: "app",
  provide: {
    [THEME_KEY]: "dark",
  },
  data() {
    return {
      width: 100,
      height: 250,
      top: 0,
      left: 0,
      // 配置可视化图形
      option: {
        title: {
          text: "Traffic Sources",
          left: "center",
        },
        tooltip: {
          trigger: "item",
          formatter: "{a} <br/>{b} : {c} ({d}%)",
        },
        legend: {
          orient: "vertical",
          left: "left",
          data: [
            "Direct",
            "Email",
            "Ad Networks",
            "Video Ads",
            "Search Engines",
          ],
        },
        series: [
          {
            name: "Traffic Sources",
            type: "pie",
            radius: "55%",
            center: ["50%", "60%"],
            data: [
              { value: 335, name: "Direct" },
              { value: 310, name: "Email" },
              { value: 234, name: "Ad Networks" },
              { value: 135, name: "Video Ads" },
              { value: 1548, name: "Search Engines" },
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
      },
    };
  },
  methods: {
    resize(newRect) {
      this.width = newRect.width;
      this.height = newRect.height;
      this.top = newRect.top;
      this.left = newRect.left;
    },
  },
};
</script>

<style scoped>
.box-card {
  height: 92%;
  position: fixed;
  overflow: auto;
  border-style: dotted;
  border-color: black;
  scroll-behavior: inherit;
}
#card1 {
  left: 0.5%;
  width: 25%;
}
#card2 {
  width: 50%;
  left: 25.5%;
}
#card3 {
  width: 20%;
  left: 75%;
}
#card4 {
  width: 5%;
  left: 94%;
}
</style>

