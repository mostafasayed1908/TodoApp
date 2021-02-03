<template>
  <div id="app">
    <div class="container">
    <img alt="Vue logo" src="./assets/logo.png">
    <TodoApp />
    </div>
  </div>
</template>

<script>
import TodoApp from './components/TodoApp.vue'

export default {
  name: 'App',
  components: {
    TodoApp
  }
}
</script>

<style>
#app {
  font-family: 'Lato', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  font-size: 20px
}
#app .container > img{
  max-width: 60px;
}
.container {
  width:600px;
  margin: 0 auto;
}
</style>
