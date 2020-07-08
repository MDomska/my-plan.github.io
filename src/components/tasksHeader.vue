<template>
  <div>
    <header class="header">
      <h1 v-if="tasks.length > 1">We have {{ tasks.length }} tasks</h1>
      <h1 v-else-if="tasks.length === 1">We have {{ tasks.length }} task</h1>
      <h1 v-else>We don't have any tasks</h1>
    </header>
  </div>
</template>
    
<script>
export default {
  props: {
    tasks: {
      type: Array,
      required: true
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