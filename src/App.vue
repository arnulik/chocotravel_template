<template>
  <div id="app"><mainform></mainform></div>
</template>

<script>
import MainForm from "./components/MainForm";

export default {
  name: "App",
  components: {
    mainform: MainForm
  }
};
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  background: #dff1ff;
}
</style>
