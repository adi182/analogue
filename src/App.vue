<template>
  <vue-clock/>
</template>

<script>
import VueClock from './components/VueClock.vue'

export default {
  name: 'App',
  components: {
    VueClock
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
