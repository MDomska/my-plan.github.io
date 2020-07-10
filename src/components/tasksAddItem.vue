<template>
  <div>
    <form @submit.prevent="addItem">
      <label>
        <input type="text" v-model="newTask" placeholder="New task" @keyup.enter="addItem" />
      </label>
      <button class="btn" type="submit">Add</button>
    </form>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      newTask: ""
    };
  },
  methods: {
    addItem() {
      this.$emit("addTask", this.newTask);
      this.newTask = "";
    }
  }
};
</script>

<style scoped>
input {
  padding: 10px 30px;
  border: #190647 4px inset;
  border-radius: 15px;
}
</style>