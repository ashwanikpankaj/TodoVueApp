<template>
  <div id="app" class="heading">
    <div>
      <h1>Todo App</h1>
      <Todo />
    </div>
  </div>
</template>

<script>
import Todo from "./components/Todo";
export default {
  name: "App",
  components: {
    Todo,
  },
};
</script>

<style>
.heading {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
