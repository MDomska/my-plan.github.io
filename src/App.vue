<template>
  <div id="app">
    <tasks-list></tasks-list>
  </div>
</template>
 
<script>
import tasksList from "./components/tasksList.vue";

export default {
  name: "App",
  components: {
    tasksList
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
