<template>
  <div id="app">
    <!-- <HelloWorld /> -->
    <MyUi />
  </div>
</template>

<script>
import MyUi from "./components/InputReplace.vue";

export default {
  name: "app",
  components: {
    MyUi,
  },
};
</script>

<style scoped>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
