<template>
  <div id="app">
    <home-view></home-view>
  </div>
</template>

<script>
import HomeView from "./views/HomeView.vue";
export default {
  name: "app",
  components: {
    HomeView,
  },
};
</script>

