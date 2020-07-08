<template>
  <div id="tasksList" class="container">
    <tasks-header :tasks="tasks" class="header" />
    <div class="wraper">
      <tasks-add-item @addTask="addTask" />
      <tasks-item :tasks="tasks" @statusChanged="statusChanged" @deleteTask="deleteTask" />
    </div>
  </div>
</template>

<script>
import tasksHeader from "./tasksHeader";
import tasksItem from "./tasksItem";
import tasksAddItem from "./tasksAddItem";

export default {
  name: "tasksList",
  components: {
    tasksHeader,
    tasksItem,
    tasksAddItem
  },
  data: function() {
    return {
      newTask: "",
      id: Date.now(),
      tasks: [
        { id: 1, text: "buy products", status: false },
        { id: 2, text: "buy tickets to Kyiv", status: false },
        { id: 3, text: "clean the floor", status: false }
      ]
    };
  },
  async mounted() {
    if (localStorage.getItem("tasks")) {
      try {
        this.tasks = await JSON.parse(localStorage.getItem("tasks"));
      } catch (e) {
        localStorage.deleteItem("tasks");
      }
    }
  },
  methods: {
    addTask(newTask) {
      if (newTask !== "") {
        this.tasks.push({
          id: this.id,
          text: this.newTask,
          status: false
        });
        this.saveTasks();
      }
      this.newTask = "";
    },
    deleteTask: function(index) {
      this.tasks.splice(index, 1);
      this.saveTasks();
    },
    saveTasks() {
      const parsed = JSON.stringify(this.tasks);
      localStorage.setItem("tasks", parsed);
    },
    statusChanged(index) {
      if (this.tasks[index].status === false) {
        this.tasks[index].status = true;
      } else {
        this.tasks[index].status = false;
      }
      this.tasks.sort((a, b) => a.status - b.status);
      this.saveTasks();
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
.header {
  width: 100%;
  padding: 20px;
  background: linear-gradient(-90deg, #190647, #16c0b0);
  color: #dddddd;
}
.wraper {
  width: 70%;
  margin: 30px auto;
}
ul {
  margin-top: 20px;
}
li {
  display: flex;
  padding: 10px;
  justify-content: space-between;
}
.btn {
  padding: 10px 20px;
  background-color: #190647;
  color: #dddddd;
  border: #dddddd outset 2px;
  margin-left: 20px;
  border-radius: 15px;
}
input {
  padding: 10px 30px;
}
.doneTask {
  text-decoration: line-through;
}
</style>
