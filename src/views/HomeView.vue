<template>
  <div id="app">
    <VueDragResize
      :isActive="true"
      :w="300"
      :h="300"
      @resizing="resize"
      @dragging="resize"
    >
      <div
        id="chart"
        ref="chart"
        :style="{ width: width + 'px', height: height + 'px' }"
      ></div>
    </VueDragResize>
  </div>
</template>

<script>
import VueDragResize from "vue-drag-resize";
export default {
  name: "app",

  components: {
    VueDragResize,
  },

  data() {
    return {
      width: 300,
      height: 300,
      top: 0,
      left: 0,
      chart: null,
      // 配置可视化图形
      option: {
        tooltip: {
          trigger: "item",
        },
        legend: {
          top: "5%",
          left: "center",
        },
        series: [
          {
            name: "Access From",
            type: "pie",
            radius: ["40%", "70%"],
            avoidLabelOverlap: false,
            itemStyle: {
              borderRadius: 10,
              borderColor: "#fff",
              borderWidth: 2,
            },
            label: {
              show: false,
              position: "center",
            },
            emphasis: {
              label: {
                show: true,
                fontSize: "40",
                fontWeight: "bold",
              },
            },
            labelLine: {
              show: false,
            },
            data: [
              { value: 1048, name: "Search Engine" },
              { value: 735, name: "Direct" },
              { value: 580, name: "Email" },
              { value: 484, name: "Union Ads" },
              { value: 300, name: "Video Ads" },
            ],
          },
        ],
      },
    };
  },
  methods: {
    getPage() {
      // 引用chart并初始化
      this.chart = this.$echarts.init(this.$refs.chart);
      // 使用刚指定的配置项和数据显示图表。
      this.chart.setOption(this.option);
    },
    resize(newRect) {
      this.width = newRect.width;
      this.height = newRect.height;
      this.top = newRect.top;
      this.left = newRect.left;
    },
  },
  created() {},
  mounted() {
    this.getPage();
    // console.log(this.test.a);
  },
};
</script>

<style scoped>
/* #chart {
  border-style: dashed;
  border-color: red;
} */
</style>