<template>
  <el-container>
    <el-main>
      <el-card>
        <draggable
          :group="{
            name: 'charts',
            pull: 'clone',
            put: false,
            revertClone: true,
          }"
          class="group"
          id="group1"
          :list="list1"
        >
          <v-chart
            v-for="(chart, index) in list1"
            :style="{ height: '30%', width: '100%' }"
            :option="chart"
            :key="index"
          />
        </draggable>
        <draggable
          :group="{ name: 'charts', pull: false, put: true, revertClone: true }"
          id="group2"
          class="group"
          :list="list2"
        >
          <vue-drag-resize
            v-for="(chart, index) in list2"
            :key="index"
            :w="380"
            :h="250"
            v-on:resizing="resize"
            v-on:dragging="resize"
          >
            <v-chart
              :style="{ height: height + 'px', width: width + 'px' }"
              :option="chart"
              :autoresize="true"
            />
          </vue-drag-resize>
        </draggable>
      </el-card>
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
      width: 380,
      height: 250,
      top: 0,
      left: 0,
      list1: [
        {
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
        {
          xAxis: {
            type: "category",
            data: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"],
          },
          yAxis: {
            type: "value",
          },
          series: [
            {
              data: [150, 230, 224, 218, 135, 147, 260],
              type: "line",
            },
          ],
        },
      ],
      list2: [],
      // 配置可视化图形
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
.el-card {
  height: 92%;
  width: 80%;
  position: fixed;
  overflow: auto;
  border-style: dotted;
  border-color: black;
  scroll-behavior: inherit;
}
.group {
  border-style: dotted;
  border-color: red;
  position: fixed;
  height: 86%;
}
#group1 {
  width: 25%;
}
#group2 {
  width: 51%;
  left: 29%;
}
</style>
