<template>
  <div id="app">
    <HeaderItem />
    <TodoList />
  </div>
</template>
<script>
import HeaderItem from './components/HeaderItem.vue';
import TodoList from './components/TodoList.vue';

export default {
  name: "App",
  components: {HeaderItem, TodoList},
}
</script>

<style>
  #app {
    font-family: Arial, Helvetica, sans-serif;
  }
</style>