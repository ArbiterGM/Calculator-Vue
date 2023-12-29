<template>
  <div id="app">
    <Calculator />
  </div>
</template>

<script>
import Calculator from './components/Calculator.vue'

export default {
  name: 'app',
  components: {
    Calculator
  }
}
</script>

<style lang="scss">
body {
  background-color: #5A7BBE;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
