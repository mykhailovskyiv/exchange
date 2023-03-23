<template>
  <div id="app">
    <main-layout></main-layout>
  </div>
</template>

<script>
import MainLayout from "./components/MainLayout";

export default {
  name: 'app',
  components: {MainLayout},
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  comments: {
    MainLayout
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}
h1,h2,h3,h4,h5,p,span {
  margin: 0;
  color: black;
  box-sizing: border-box;
}
body {
  margin: 0;
}

</style>
