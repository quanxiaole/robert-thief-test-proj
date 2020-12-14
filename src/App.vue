<template>
  <div id="app">
    <!-- <h3>萝卜小贼的测试项目</h3> -->
    <source-data></source-data>
    <hr>
    <data-view></data-view>
  </div>
</template>

<script>
import SourceData from './components/SourceData.vue';
import DataView from './components/DataView.vue';

export default {
  name: 'App',
  components: {
    SourceData,
    DataView,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 20px;
}
</style>
