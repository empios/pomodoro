<template>
  <div id="app">
    <Clock/>
  </div>
</template>

<script>
import Clock from './components/Clock.vue'

export default {
  name: 'App',
  components: {
    Clock
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
  position: fixed;
  top: 50%;
  left: 50%;
  /* bring your own prefixes */
  transform: translate(-50%, -50%);

}
html{
  height: 100%;
}
body{
  height: 100%!important;
}
</style>
