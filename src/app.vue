<template>
  <div id="app">
    <main-layout></main-layout>
    <footer class="footer">
      <span>© {{ this.year }} Valerii Mykhailovskyi | All rights reserved</span>
    </footer>
  </div>
</template>

<script>
import MainLayout from "./components/MainLayout";

export default {
  name: 'app',
  components: {MainLayout},
  data () {
    return {
      year: new Date().getFullYear()
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
  color: #ffffff;
  box-sizing: border-box;
}
body {
  margin: 0;
  background-color: #1f1f1f;;
}
.footer {
  margin: 20px 0;
  position: absolute;
  bottom: 0;
  right: 0;
  left: 0;
  span {
    font-size: 13px;
    color: #ffffff;
  }
}

</style>
