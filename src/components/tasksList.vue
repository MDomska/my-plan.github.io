<template>
  <div class="container">
    <tasks-header :numOfTasks="tasks.length" />
    <div class="wraper">
      <tasks-add-item @addTask="addTask($event)" />
      <tasks-list-items :tasks="tasks" @statusChanged="statusChanged" @deleteTask="deleteTask" />
    </div>
  </div>
</template>

<script>
import TasksHeader from "./TasksHeader";
import TasksListItems from "./TasksListItems";
import TasksAddItem from "./TasksAddItem";

export default {
  name: "TasksList",
  components: {
    TasksHeader,
    TasksListItems,
    TasksAddItem
  },
  data: function() {
    return {
      tasks: [
        { id: 1, text: "buy products", status: false },
        { id: 2, text: "buy tickets to Kyiv", status: false },
        { id: 3, text: "clean the floor", status: false }
      ]
    };
  },
  mounted() {
    if (localStorage.getItem("tasks")) {
      try {
        this.tasks = JSON.parse(localStorage.getItem("tasks"));
      } catch (e) {
        localStorage.removeItem("tasks");
      }
    }
  },
  methods: {
    addTask(newTask) {
      if (newTask !== "") {
        this.tasks.unshift({
          id: Date.now(),
          text: newTask,
          status: false
        });
        this.updateTasks();
      }
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
      this.updateTasks();
    },
    saveTasks() {
      const parsed = JSON.stringify(this.tasks);
      localStorage.setItem("tasks", parsed);
    },
    updateTasks() {
      this.tasks.sort((a, b) => a.status - b.status);
      this.saveTasks();
    },
    statusChanged(index) {
      if (this.tasks[index].status === false) {
        this.tasks[index].status = true;
      } else {
        this.tasks[index].status = false;
      }
      this.updateTasks();
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.container {
  width: 80%;
  margin: 0 auto;
  background-color: #e0fdfb;
}
@media screen and (max-width: 787px) {
  .container {
    width: 100%;
  }
  .wraper {
    width: 100%;
  }
  input {
    padding: 10px;
  }
}
.wraper {
  width: 70%;
  margin: 30px auto;
}
</style>
