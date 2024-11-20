<template>
    <div class="box">
      <h1 class="subtitle" style="color: greenyellow;">Add a Task</h1>
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
          date: '',
        },
      };
    },
    methods: {
      submitForm() {
        this.$emit('add-task', { ...this.newTask });
        this.newTask = { title: '', category: '', date: '' };
      },
    },
  };
</script>

  