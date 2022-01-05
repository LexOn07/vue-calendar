<template>
  <div id="app">
    <img src="./assets/logo.png">
    <HelloWorld enableNavButton date="2022-01-01" class="HelloWorld" />
  </div>
</template>

<script>
import HelloWorld from './components/vue-calendar'

export default {
  name: 'App',
  components: {
    HelloWorld
  }
}
</script>

<style>
.HelloWorld{
  width: 400px;
  height: 500px;
  background: orange;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
