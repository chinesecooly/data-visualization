<template>
  <div id="app">
    <vue-drag-resize
      :w="380"
      :h="195"
      @resizing="resize"
      v-on="dragstopListener"
    >
      <v-chart
        :style="{ height: height, width: width }"
        :option="chart"
        :autoresize="true"
      />
    </vue-drag-resize>
  </div>
</template>

<script>
export default {
  name: "DraggableResizeChart",
  props: {
    chart: {
      type: Object,
      default: function () {
        return {};
      },
    },
  },
  data() {
    return {
      width: "100%",
      height: "100%",
    };
  },
  computed: {
    dragstopListener: function () {
      // `Object.assign` 将所有的对象合并为一个新对象
      return Object.assign(
        {},
        // 我们从父级添加所有的监听器
        this.$listeners
      );
    },
  },
  methods: {
    resize(newRect) {
      this.width = newRect.width;
      this.height = newRect.height;
    },
  },
};
</script>

<style scoped></style>
