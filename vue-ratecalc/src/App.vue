<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
  <RateCalculator />
</template>

<script>
import RateCalculator from './components/RateCalculator.vue'

export default {
  name: 'App',
  components: {
    RateCalculator
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
