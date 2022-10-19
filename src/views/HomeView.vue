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
            :style="{ height: '30%', width: '100%', marginBottom: '10px' }"
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
        {
          title: {
            text: "Stacked Area Chart",
          },
          tooltip: {
            trigger: "axis",
            axisPointer: {
              type: "cross",
              label: {
                backgroundColor: "#6a7985",
              },
            },
          },
          legend: {
            data: [
              "Email",
              "Union Ads",
              "Video Ads",
              "Direct",
              "Search Engine",
            ],
          },
          toolbox: {
            feature: {
              saveAsImage: {},
            },
          },
          grid: {
            left: "3%",
            right: "4%",
            bottom: "3%",
            containLabel: true,
          },
          xAxis: [
            {
              type: "category",
              boundaryGap: false,
              data: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"],
            },
          ],
          yAxis: [
            {
              type: "value",
            },
          ],
          series: [
            {
              name: "Email",
              type: "line",
              stack: "Total",
              areaStyle: {},
              emphasis: {
                focus: "series",
              },
              data: [120, 132, 101, 134, 90, 230, 210],
            },
            {
              name: "Union Ads",
              type: "line",
              stack: "Total",
              areaStyle: {},
              emphasis: {
                focus: "series",
              },
              data: [220, 182, 191, 234, 290, 330, 310],
            },
            {
              name: "Video Ads",
              type: "line",
              stack: "Total",
              areaStyle: {},
              emphasis: {
                focus: "series",
              },
              data: [150, 232, 201, 154, 190, 330, 410],
            },
            {
              name: "Direct",
              type: "line",
              stack: "Total",
              areaStyle: {},
              emphasis: {
                focus: "series",
              },
              data: [320, 332, 301, 334, 390, 330, 320],
            },
            {
              name: "Search Engine",
              type: "line",
              stack: "Total",
              label: {
                show: true,
                position: "top",
              },
              areaStyle: {},
              emphasis: {
                focus: "series",
              },
              data: [820, 932, 901, 934, 1290, 1330, 1320],
            },
          ],
        },
        {
          title: [
            {
              text: "Tangential Polar Bar Label Position (middle)",
            },
          ],
          polar: {
            radius: [30, "80%"],
          },
          angleAxis: {
            max: 4,
            startAngle: 75,
          },
          radiusAxis: {
            type: "category",
            data: ["a", "b", "c", "d"],
          },
          tooltip: {},
          series: {
            type: "bar",
            data: [2, 1.2, 2.4, 3.6],
            coordinateSystem: "polar",
            label: {
              show: true,
              position: "middle",
              formatter: "{b}: {c}",
            },
          },
        },
        {
          tooltip: {
            trigger: "axis",
            axisPointer: {
              // Use axis to trigger tooltip
              type: "shadow", // 'shadow' as default; can also be 'line' or 'shadow'
            },
          },
          legend: {},
          grid: {
            left: "3%",
            right: "4%",
            bottom: "3%",
            containLabel: true,
          },
          xAxis: {
            type: "value",
          },
          yAxis: {
            type: "category",
            data: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"],
          },
          series: [
            {
              name: "Direct",
              type: "bar",
              stack: "total",
              label: {
                show: true,
              },
              emphasis: {
                focus: "series",
              },
              data: [320, 302, 301, 334, 390, 330, 320],
            },
            {
              name: "Mail Ad",
              type: "bar",
              stack: "total",
              label: {
                show: true,
              },
              emphasis: {
                focus: "series",
              },
              data: [120, 132, 101, 134, 90, 230, 210],
            },
            {
              name: "Affiliate Ad",
              type: "bar",
              stack: "total",
              label: {
                show: true,
              },
              emphasis: {
                focus: "series",
              },
              data: [220, 182, 191, 234, 290, 330, 310],
            },
            {
              name: "Video Ad",
              type: "bar",
              stack: "total",
              label: {
                show: true,
              },
              emphasis: {
                focus: "series",
              },
              data: [150, 212, 201, 154, 190, 330, 410],
            },
            {
              name: "Search Engine",
              type: "bar",
              stack: "total",
              label: {
                show: true,
              },
              emphasis: {
                focus: "series",
              },
              data: [820, 832, 901, 934, 1290, 1330, 1320],
            },
          ],
        },
        {
          xAxis: {
            data: ["2017-10-24", "2017-10-25", "2017-10-26", "2017-10-27"],
          },
          yAxis: {},
          series: [
            {
              type: "candlestick",
              data: [
                [20, 34, 10, 38],
                [40, 35, 30, 50],
                [31, 38, 33, 44],
                [38, 15, 5, 42],
              ],
            },
          ],
        },
        {
          title: {
            text: "Basic Radar Chart",
          },
          legend: {
            data: ["Allocated Budget", "Actual Spending"],
          },
          radar: {
            // shape: 'circle',
            indicator: [
              { name: "Sales", max: 6500 },
              { name: "Administration", max: 16000 },
              { name: "Information Technology", max: 30000 },
              { name: "Customer Support", max: 38000 },
              { name: "Development", max: 52000 },
              { name: "Marketing", max: 25000 },
            ],
          },
          series: [
            {
              name: "Budget vs spending",
              type: "radar",
              data: [
                {
                  value: [4200, 3000, 20000, 35000, 50000, 18000],
                  name: "Allocated Budget",
                },
                {
                  value: [5000, 14000, 28000, 26000, 42000, 21000],
                  name: "Actual Spending",
                },
              ],
            },
          ],
        },
        {
          title: {
            text: "Basic Graph",
          },
          tooltip: {},
          animationDurationUpdate: 1500,
          animationEasingUpdate: "quinticInOut",
          series: [
            {
              type: "graph",
              layout: "none",
              symbolSize: 50,
              roam: true,
              label: {
                show: true,
              },
              edgeSymbol: ["circle", "arrow"],
              edgeSymbolSize: [4, 10],
              edgeLabel: {
                fontSize: 20,
              },
              data: [
                {
                  name: "Node 1",
                  x: 300,
                  y: 300,
                },
                {
                  name: "Node 2",
                  x: 800,
                  y: 300,
                },
                {
                  name: "Node 3",
                  x: 550,
                  y: 100,
                },
                {
                  name: "Node 4",
                  x: 550,
                  y: 500,
                },
              ],
              // links: [],
              links: [
                {
                  source: 0,
                  target: 1,
                  symbolSize: [5, 20],
                  label: {
                    show: true,
                  },
                  lineStyle: {
                    width: 5,
                    curveness: 0.2,
                  },
                },
                {
                  source: "Node 2",
                  target: "Node 1",
                  label: {
                    show: true,
                  },
                  lineStyle: {
                    curveness: 0.2,
                  },
                },
                {
                  source: "Node 1",
                  target: "Node 3",
                },
                {
                  source: "Node 2",
                  target: "Node 3",
                },
                {
                  source: "Node 2",
                  target: "Node 4",
                },
                {
                  source: "Node 1",
                  target: "Node 4",
                },
              ],
              lineStyle: {
                opacity: 0.9,
                width: 2,
                curveness: 0,
              },
            },
          ],
        },
        {
          parallelAxis: [
            { dim: 0, name: "Price" },
            { dim: 1, name: "Net Weight" },
            { dim: 2, name: "Amount" },
            {
              dim: 3,
              name: "Score",
              type: "category",
              data: ["Excellent", "Good", "OK", "Bad"],
            },
          ],
          series: {
            type: "parallel",
            lineStyle: {
              width: 4,
            },
            data: [
              [12.99, 100, 82, "Good"],
              [9.99, 80, 77, "OK"],
              [20, 120, 60, "Excellent"],
            ],
          },
        },
        {
          series: {
            type: "sankey",
            layout: "none",
            emphasis: {
              focus: "adjacency",
            },
            data: [
              {
                name: "a",
              },
              {
                name: "b",
              },
              {
                name: "a1",
              },
              {
                name: "a2",
              },
              {
                name: "b1",
              },
              {
                name: "c",
              },
            ],
            links: [
              {
                source: "a",
                target: "a1",
                value: 5,
              },
              {
                source: "a",
                target: "a2",
                value: 3,
              },
              {
                source: "b",
                target: "b1",
                value: 8,
              },
              {
                source: "a",
                target: "b1",
                value: 3,
              },
              {
                source: "b1",
                target: "a1",
                value: 1,
              },
              {
                source: "b1",
                target: "c",
                value: 2,
              },
            ],
          },
        },
        {
          title: {
            text: "Funnel Compare",
            subtext: "Fake Data",
            left: "left",
            top: "bottom",
          },
          tooltip: {
            trigger: "item",
            formatter: "{a} <br/>{b} : {c}%",
          },
          toolbox: {
            show: true,
            orient: "vertical",
            top: "center",
            feature: {
              dataView: { readOnly: false },
              restore: {},
              saveAsImage: {},
            },
          },
          legend: {
            orient: "vertical",
            left: "left",
            data: ["Prod A", "Prod B", "Prod C", "Prod D", "Prod E"],
          },
          series: [
            {
              name: "Funnel",
              type: "funnel",
              width: "40%",
              height: "45%",
              left: "5%",
              top: "50%",
              funnelAlign: "right",
              data: [
                { value: 60, name: "Prod C" },
                { value: 30, name: "Prod D" },
                { value: 10, name: "Prod E" },
                { value: 80, name: "Prod B" },
                { value: 100, name: "Prod A" },
              ],
            },
            {
              name: "Pyramid",
              type: "funnel",
              width: "40%",
              height: "45%",
              left: "5%",
              top: "5%",
              sort: "ascending",
              funnelAlign: "right",
              data: [
                { value: 60, name: "Prod C" },
                { value: 30, name: "Prod D" },
                { value: 10, name: "Prod E" },
                { value: 80, name: "Prod B" },
                { value: 100, name: "Prod A" },
              ],
            },
            {
              name: "Funnel",
              type: "funnel",
              width: "40%",
              height: "45%",
              left: "55%",
              top: "5%",
              funnelAlign: "left",
              data: [
                { value: 60, name: "Prod C" },
                { value: 30, name: "Prod D" },
                { value: 10, name: "Prod E" },
                { value: 80, name: "Prod B" },
                { value: 100, name: "Prod A" },
              ],
            },
            {
              name: "Pyramid",
              type: "funnel",
              width: "40%",
              height: "45%",
              left: "55%",
              top: "50%",
              sort: "ascending",
              funnelAlign: "left",
              data: [
                { value: 60, name: "Prod C" },
                { value: 30, name: "Prod D" },
                { value: 10, name: "Prod E" },
                { value: 80, name: "Prod B" },
                { value: 100, name: "Prod A" },
              ],
            },
          ],
        },
        {
          tooltip: {
            formatter: "{a} <br/>{b} : {c}%",
          },
          series: [
            {
              name: "Pressure",
              type: "gauge",
              detail: {
                formatter: "{value}",
              },
              data: [
                {
                  value: 50,
                  name: "SCORE",
                },
              ],
            },
          ],
        },
        {
          tooltip: {
            trigger: "axis",
            axisPointer: {
              type: "line",
              lineStyle: {
                color: "rgba(0,0,0,0.2)",
                width: 1,
                type: "solid",
              },
            },
          },
          legend: {
            data: ["DQ", "TY", "SS", "QG", "SY", "DD"],
          },
          singleAxis: {
            top: 50,
            bottom: 50,
            axisTick: {},
            axisLabel: {},
            type: "time",
            axisPointer: {
              animation: true,
              label: {
                show: true,
              },
            },
            splitLine: {
              show: true,
              lineStyle: {
                type: "dashed",
                opacity: 0.2,
              },
            },
          },
          series: [
            {
              type: "themeRiver",
              emphasis: {
                itemStyle: {
                  shadowBlur: 20,
                  shadowColor: "rgba(0, 0, 0, 0.8)",
                },
              },
              data: [
                ["2015/11/08", 10, "DQ"],
                ["2015/11/09", 15, "DQ"],
                ["2015/11/10", 35, "DQ"],
                ["2015/11/11", 38, "DQ"],
                ["2015/11/12", 22, "DQ"],
                ["2015/11/13", 16, "DQ"],
                ["2015/11/14", 7, "DQ"],
                ["2015/11/15", 2, "DQ"],
                ["2015/11/16", 17, "DQ"],
                ["2015/11/17", 33, "DQ"],
                ["2015/11/18", 40, "DQ"],
                ["2015/11/19", 32, "DQ"],
                ["2015/11/20", 26, "DQ"],
                ["2015/11/21", 35, "DQ"],
                ["2015/11/22", 40, "DQ"],
                ["2015/11/23", 32, "DQ"],
                ["2015/11/24", 26, "DQ"],
                ["2015/11/25", 22, "DQ"],
                ["2015/11/26", 16, "DQ"],
                ["2015/11/27", 22, "DQ"],
                ["2015/11/28", 10, "DQ"],
                ["2015/11/08", 35, "TY"],
                ["2015/11/09", 36, "TY"],
                ["2015/11/10", 37, "TY"],
                ["2015/11/11", 22, "TY"],
                ["2015/11/12", 24, "TY"],
                ["2015/11/13", 26, "TY"],
                ["2015/11/14", 34, "TY"],
                ["2015/11/15", 21, "TY"],
                ["2015/11/16", 18, "TY"],
                ["2015/11/17", 45, "TY"],
                ["2015/11/18", 32, "TY"],
                ["2015/11/19", 35, "TY"],
                ["2015/11/20", 30, "TY"],
                ["2015/11/21", 28, "TY"],
                ["2015/11/22", 27, "TY"],
                ["2015/11/23", 26, "TY"],
                ["2015/11/24", 15, "TY"],
                ["2015/11/25", 30, "TY"],
                ["2015/11/26", 35, "TY"],
                ["2015/11/27", 42, "TY"],
                ["2015/11/28", 42, "TY"],
                ["2015/11/08", 21, "SS"],
                ["2015/11/09", 25, "SS"],
                ["2015/11/10", 27, "SS"],
                ["2015/11/11", 23, "SS"],
                ["2015/11/12", 24, "SS"],
                ["2015/11/13", 21, "SS"],
                ["2015/11/14", 35, "SS"],
                ["2015/11/15", 39, "SS"],
                ["2015/11/16", 40, "SS"],
                ["2015/11/17", 36, "SS"],
                ["2015/11/18", 33, "SS"],
                ["2015/11/19", 43, "SS"],
                ["2015/11/20", 40, "SS"],
                ["2015/11/21", 34, "SS"],
                ["2015/11/22", 28, "SS"],
                ["2015/11/23", 26, "SS"],
                ["2015/11/24", 37, "SS"],
                ["2015/11/25", 41, "SS"],
                ["2015/11/26", 46, "SS"],
                ["2015/11/27", 47, "SS"],
                ["2015/11/28", 41, "SS"],
                ["2015/11/08", 10, "QG"],
                ["2015/11/09", 15, "QG"],
                ["2015/11/10", 35, "QG"],
                ["2015/11/11", 38, "QG"],
                ["2015/11/12", 22, "QG"],
                ["2015/11/13", 16, "QG"],
                ["2015/11/14", 7, "QG"],
                ["2015/11/15", 2, "QG"],
                ["2015/11/16", 17, "QG"],
                ["2015/11/17", 33, "QG"],
                ["2015/11/18", 40, "QG"],
                ["2015/11/19", 32, "QG"],
                ["2015/11/20", 26, "QG"],
                ["2015/11/21", 35, "QG"],
                ["2015/11/22", 40, "QG"],
                ["2015/11/23", 32, "QG"],
                ["2015/11/24", 26, "QG"],
                ["2015/11/25", 22, "QG"],
                ["2015/11/26", 16, "QG"],
                ["2015/11/27", 22, "QG"],
                ["2015/11/28", 10, "QG"],
                ["2015/11/08", 10, "SY"],
                ["2015/11/09", 15, "SY"],
                ["2015/11/10", 35, "SY"],
                ["2015/11/11", 38, "SY"],
                ["2015/11/12", 22, "SY"],
                ["2015/11/13", 16, "SY"],
                ["2015/11/14", 7, "SY"],
                ["2015/11/15", 2, "SY"],
                ["2015/11/16", 17, "SY"],
                ["2015/11/17", 33, "SY"],
                ["2015/11/18", 40, "SY"],
                ["2015/11/19", 32, "SY"],
                ["2015/11/20", 26, "SY"],
                ["2015/11/21", 35, "SY"],
                ["2015/11/22", 4, "SY"],
                ["2015/11/23", 32, "SY"],
                ["2015/11/24", 26, "SY"],
                ["2015/11/25", 22, "SY"],
                ["2015/11/26", 16, "SY"],
                ["2015/11/27", 22, "SY"],
                ["2015/11/28", 10, "SY"],
                ["2015/11/08", 10, "DD"],
                ["2015/11/09", 15, "DD"],
                ["2015/11/10", 35, "DD"],
                ["2015/11/11", 38, "DD"],
                ["2015/11/12", 22, "DD"],
                ["2015/11/13", 16, "DD"],
                ["2015/11/14", 7, "DD"],
                ["2015/11/15", 2, "DD"],
                ["2015/11/16", 17, "DD"],
                ["2015/11/17", 33, "DD"],
                ["2015/11/18", 4, "DD"],
                ["2015/11/19", 32, "DD"],
                ["2015/11/20", 26, "DD"],
                ["2015/11/21", 35, "DD"],
                ["2015/11/22", 40, "DD"],
                ["2015/11/23", 32, "DD"],
                ["2015/11/24", 26, "DD"],
                ["2015/11/25", 22, "DD"],
                ["2015/11/26", 16, "DD"],
                ["2015/11/27", 22, "DD"],
                ["2015/11/28", 10, "DD"],
              ],
            },
          ],
        },
        {
          legend: {},
          tooltip: {},
          dataset: {
            source: [
              ["product", "2012", "2013", "2014", "2015", "2016", "2017"],
              ["Milk Tea", 86.5, 92.1, 85.7, 83.1, 73.4, 55.1],
              ["Matcha Latte", 41.1, 30.4, 65.1, 53.3, 83.8, 98.7],
              ["Cheese Cocoa", 24.1, 67.2, 79.5, 86.4, 65.2, 82.5],
              ["Walnut Brownie", 55.2, 67.1, 69.2, 72.4, 53.9, 39.1],
            ],
          },
          series: [
            {
              type: "pie",
              radius: "20%",
              center: ["25%", "30%"],
              // No encode specified, by default, it is '2012'.
            },
            {
              type: "pie",
              radius: "20%",
              center: ["75%", "30%"],
              encode: {
                itemName: "product",
                value: "2013",
              },
            },
            {
              type: "pie",
              radius: "20%",
              center: ["25%", "75%"],
              encode: {
                itemName: "product",
                value: "2014",
              },
            },
            {
              type: "pie",
              radius: "20%",
              center: ["75%", "75%"],
              encode: {
                itemName: "product",
                value: "2015",
              },
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
  /* border-style: dotted;
  border-color: red; */
  position: fixed;
  height: 86%;
}
#group1 {
  width: 25%;
  overflow: auto;
}
#group2 {
  width: 51%;
  left: 29%;
}
#group1::-webkit-scrollbar {
  display: none;
}
</style>
