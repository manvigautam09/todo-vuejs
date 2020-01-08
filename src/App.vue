<template>
  <div id="app">
    <Todo title="ToDos" />
  </div>
</template>
<script>
import Todo from "./components/Todo.vue";
export default {
  name: "app",
  components: {
    Todo
  }
};
</script>

<style>
#app {
  height: 100vh;
  background-color: #f5f5f5;
}
</style>
