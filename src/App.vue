<template>
  <div id="app">
    <Main />
  </div>
</template>

<script>
import Main from './components/macro/Main.vue';

export default {
  name: 'App',
  components: {
    Main
  }
}
</script>

<style lang="scss">
body{
  box-sizing: border-box;
  margin:0;
  padding: 0;
  background-color: rgb(44, 37, 37);
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
