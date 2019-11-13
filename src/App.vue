<template>
  <div id="app">
    <ApiStuff/>
  </div>
</template>

<script>
import ApiStuff from './components/ApiStuff.vue'

export default {
  name: 'app',
  components: {
   ApiStuff
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
