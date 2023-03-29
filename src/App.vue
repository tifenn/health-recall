<template>
  <img alt="Recall Logo" src="./assets/recall.png">
  <HealthRecall msg="Welcome to Health Canada Recall App"/>
</template>

<script>
import HealthRecall from './components/HealthRecall.vue'

export default {
  name: 'App',
  components: {
    HealthRecall
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
