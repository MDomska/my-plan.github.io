<template>
  <div>
    <ul class="task">
      <li class="task-item" v-for="(task, index) in tasks" :key="task.id">
        <input
          type="checkbox"
          :name="task.id"
          :id="task.id"
          @click="statusItem(index)"
          :checked="task.status"
        />
        <p :class="{ taskDone: task.status }">{{ task.text }}</p>
        <button class="btn" type="button" @click="deleteItem(index)">delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    tasks: {
      type: Array,
      required: true
    }
  },
  methods: {
    statusItem(index) {
      this.$emit("statusChanged", index);
    },
    deleteItem(index) {
      this.$emit("deleteTask", index);
    }
  }
};
</script>

<style>
.task {
  margin-top: 20px;
}
.task-item {
  display: flex;
  padding: 10px;
  justify-content: space-between;
}
.btn {
  padding: 10px 20px;
  background-color: #060e4e;
  color: #dddddd;
  border-radius: 20px;
  margin-left: 20px;
}
.taskDone {
  text-decoration: line-through;
}
</style>