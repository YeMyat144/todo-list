<template>
    <div class="box">
      <h2 class="subtitle" style="color: greenyellow;">Add a Task</h2>
      <form @submit.prevent="submitForm">
        <div class="field">
          <label class="label">Title</label>
          <div class="control">
            <input
              class="input"
              type="text"
              v-model="newTask.title"
              placeholder="Task title"
              required
            />
          </div>
        </div>
  
        <div class="field">
          <label class="label">Category</label>
          <div class="control">
            <input
              class="input"
              type="text"
              v-model="newTask.category"
              placeholder="Category"
              required
            />
          </div>
        </div>
  
        <div class="field">
          <label class="label">Priority</label>
          <div class="select">
            <select v-model="newTask.priority" required>
              <option value="Low">Low</option>
              <option value="Medium">Medium</option>
              <option value="High">High</option>
            </select>
          </div>
        </div>
  
        <div class="field">
          <label class="label">Due Date</label>
          <div class="control">
            <input
              class="input"
              type="date"
              v-model="newTask.date"
              required
            />
          </div>
        </div>
  
        <div class="control">
          <button class="button is-primary" type="submit">Add Task</button>
        </div>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        newTask: {
          title: '',
          category: '',
          priority: 'Low',
          date: '',
        },
      };
    },
    methods: {
      submitForm() {
        this.$emit('add-task', { ...this.newTask });
        this.newTask = { title: '', category: '', priority: 'Low', date: '' };
      },
    },
  };
  </script>
  