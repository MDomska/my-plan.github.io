<template>
  <div>
    <header>
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
      type: Object,
      required: true
    }
  }
};
</script>