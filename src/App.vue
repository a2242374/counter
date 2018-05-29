<template>
  <div id="app">
    <div class="wrapper">
      <result-box></result-box>
    </div>
  </div>
</template>

<script>
import resultBox from './components/resultBox.vue'
export default {
  name: 'App',
  components: {
    resultBox
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
