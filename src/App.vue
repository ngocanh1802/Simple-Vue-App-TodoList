<template>
  <div id="app">
    <HeaderApp />
    <TodoList/>
  </div>
</template>

<script>
import HeaderApp from './components/Header';
import TodoList from './components/Todos';

export default {
  name: 'App',
  components: { HeaderApp, TodoList },
}
</script>

<style>
#app {
  max-width: 800px;
  margin: auto;
  background-color:rgb(200, 214, 235);
  padding: 10px 30px;
}
</style>