<template>
  <div>
    <form @submit.prevent="addItem(newTask)">
      <label>
        <input type="text" v-model="newTask" placeholder="New task" @keyup.enter="addItem(newTask)" />
      </label>
      <button class="btn" @click="addItem(newTask)" type="button">Add</button>
    </form>
  </div>
</template>

<script>
export default {
  props: {
    tasks: {
      type: Object,
      required: true
    },
    addTask: {
      type: Function
    },
    newTask: {
      type: String,
      required: true
    }
  },
  methods: {
    addItem(newTask) {
      this.$emit("addTask", newTask);
    }
  }
};
</script>