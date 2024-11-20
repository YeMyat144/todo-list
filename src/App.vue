<template>
  <div class="container mt-5">
    <h1 class="title has-text-centered">To-Do List</h1>

    <div class="box">
      <h2 class="subtitle">Add a Task</h2>
      <form @submit.prevent="addTask">
        <div class="field">
          <label class="label">Title</label>
          <div class="control">
            <input class="input" type="text" v-model="newTask.title" placeholder="Task title" required />
          </div>
        </div>

        <div class="field">
          <label class="label">Category</label>
          <div class="control">
            <input class="input" type="text" v-model="newTask.category" placeholder="Category" required />
          </div>
        </div>

        <div class="field">
          <label class="label">Due Date</label>
          <div class="control">
            <input class="input" type="date" v-model="newTask.date" required />
          </div>
        </div>

        <div class="control">
          <button class="button is-primary" type="submit">Add Task</button>
        </div>
      </form>
    </div>

    <div v-if="tasks.length" class="box mt-4">
      <h2 class="subtitle">Task List</h2>
      <div class="table-container">
        <table class="table is-fullwidth">
          <thead>
            <tr>
              <th>Title</th>
              <th>Category</th>
              <th>Due Date</th>
              <th>Actions</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(task, index) in tasks" :key="index">
              <td>
                <input class="input is-small" v-model="task.title" @change="updateTask(index)" />
              </td>
              <td>
                <input class="input is-small" v-model="task.category" @change="updateTask(index)" />
              </td>
              <td>
                <input class="input is-small" type="date" v-model="task.date" @change="updateTask(index)" />
              </td>
              <td>
                <button class="button is-danger is-small" @click="deleteTask(index)">Delete</button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>

    <div v-else class="notification is-info">
      No tasks available. Add a new task to get started!
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: {
        title: '',
        category: '',
        date: '',
      },
      tasks: [],
    };
  },
  created() {
    const savedTasks = JSON.parse(localStorage.getItem('tasks'));
    if (savedTasks) this.tasks = savedTasks;
  },
  methods: {
    addTask() {
      if (this.newTask.title && this.newTask.category && this.newTask.date) {
        this.tasks.push({ ...this.newTask });
        this.saveTasks();
        this.newTask = { title: '', category: '', date: '' };
      }
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
      this.saveTasks();
    },
    updateTask() {
      this.saveTasks();
    },
    saveTasks() {
      localStorage.setItem('tasks', JSON.stringify(this.tasks));
    },
  },
};
</script>

<style>

body {
  background-color: #050505;
  height: 100vh ;
}
.container {
  max-width: 800px;
}
</style>
