<template>
  <div id="tasksList" class="container">
    <header>
      <h1 v-if="tasks.length > 1">We have {{ tasks.length }} tasks</h1>
      <h1 v-else-if="tasks.length === 1">We have {{ tasks.length }} task</h1>
      <h1 v-else>We don't have any tasks</h1>
    </header>
    <div class="wraper">
      <div>
        <form>
          <label>
            <input type="text" v-model="newTask" placeholder="New task" @keyup.enter="addTask" />
          </label>
          <button class="btn" @click="addTask" type="button">Add</button>
        </form>
      </div>
      <div>
        <ul>
          <li v-for="(task, index) in tasks" :key="index">
            <input type="checkbox" @change="statusChanged(index)" />
            <p :class="{ doneTask: task.status }">{{ task.text }}</p>
            <button class="btn" type="button" @click="deleteTask(index)">delete</button>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "tasksList",
  data: function() {
    return {
      newTask: "",
      tasks: [
        { text: "buy products", status: false },
        { text: "buy tickets to Kyiv", status: false },
        { text: "clean the floor", status: false }
      ]
    };
  },
  methods: {
    addTask(newTask) {
      if (newTask !== "") {
        this.tasks.push({
          text: this.newTask,
          status: false
        });
      }
      this.newTask = "";
    },
    deleteTask: function(index) {
      this.tasks.splice(index, 1);
    },
    statusChanged(index) {
      if (this.tasks[index].status === false) {
        this.tasks[index].status = true;
      } else {
        this.tasks[index].status = false;
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  width: 80%;
  margin: 0 auto;
  background-color: #e0fdfb;
}
@media screen and (max-width: 787px) {
}
header {
  padding: 20px;
  background: linear-gradient(-90deg, #190647, #16c0b0);
  color: #dddddd;
}
.wraper {
  width: 70%;
  margin: 30px auto;
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
  border: #dddddd outset 3px;
}
input {
  padding: 10px;
}
.doneTask {
  text-decoration: line-through;
}
</style>
