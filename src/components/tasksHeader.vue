<template>
  <div>
    <header class="header">
      <h1 v-if="numOfTasks > 1">I have {{ numOfTasks }} tasks</h1>
      <h1 v-else-if="numOfTasks === 1">I have {{ numOfTasks }} task</h1>
      <h1 v-else>I don't have any tasks</h1>
    </header>
  </div>
</template>
    
<script>
export default {
  props: {
    numOfTasks: {
      type: Number,
      default: 0
    }
  }
};
</script>

<style scoped>
.header {
  width: 100%;
  padding: 20px;
  background: linear-gradient(-90deg, #190647, #16c0b0);
  color: #dddddd;
}
</style>