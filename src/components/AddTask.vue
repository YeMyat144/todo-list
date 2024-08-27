<template>
  <div class="add-task">
    <input
      v-model="newTask.name"
      type="text"
      placeholder="Add a new task"
      @keyup.enter="submitTask"
    />
    <input
      v-model="newTask.category"
      type="text"
      placeholder="Category"
    />
    <input
      v-model="newTask.dueDate"
      type="date"
    />
    <button @click="submitTask">Add Task</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: {
        name: '',
        category: '',
        dueDate: '',
        completed: false,
      },
    };
  },
  methods: {
    submitTask() {
      if (this.newTask.name.trim()) {
        this.$emit('addTask', { ...this.newTask });
        this.newTask.name = '';
        this.newTask.category = '';
        this.newTask.dueDate = '';
      }
    },
  },
};
</script>

<style scoped>
.add-task {
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
}

input {
  flex: 1;
  padding: 10px;
  margin-right: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

button {
  padding: 10px 20px;
  background-color: #28a745;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: #218838;
}
</style>