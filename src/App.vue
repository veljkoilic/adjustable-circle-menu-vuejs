<template>
  <div id="app">
      <h1>ADJUSTABLE VUE.js MENU</h1>
    <CircleMenu/>
  </div>
</template>

<script>
import CircleMenu from './components/CircleMenu.vue'

export default {
  name: 'app',
  components: {
      CircleMenu
  }
}
</script>

<style lang="scss">
body{
    margin: 0;
    padding: 0;
    background: #22181C;
    color: #fff;
}
#app {
  font-family: 'Work Sans', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
    h1{
        color: #53A548;
        text-align: center;
        margin: 80px 0;
    }


}
</style>
