<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <TodoList/>
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue'

export default {
  name: 'App',
  components: {
    TodoList
  }
}
</script>

<style>
</style>
