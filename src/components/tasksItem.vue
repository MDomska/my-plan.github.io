<template>
  <div>
    <ul>
      <li v-for="(task, index) in tasks" :key="task.id">
        <input
          type="checkbox"
          :name="task.id"
          :id="task.id"
          @click="statusItem(index)"
          :checked="task.status"
        />
        <p :class="{ doneTask: task.status }">{{ task.text }}</p>
        <button class="btn" type="button" @click="deleteItem(index)">delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    tasks: {
      type: Object,
      required: true
    },
    statusChanged: {
      type: Function
    },
    deleteTask: {
      type: Function
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