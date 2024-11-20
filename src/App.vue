<template>
  <div class="container">
    <br>
    <h1 class="title has-text-centered ">To Do List</h1>

    <TaskForm @add-task="addTask" />
    <TaskList 
      :tasks="tasks" 
      @delete-task="deleteTask" 
      @update-task="updateTask" 
    />
  </div>
</template>

<script>
import TaskForm from './components/TaskForm.vue';
import TaskList from './components/TaskList.vue';

export default {
  components: {
    TaskForm,
    TaskList,
  },
  data() {
    return {
      tasks: [],
    };
  },
  created() {
    const savedTasks = JSON.parse(localStorage.getItem('tasks'));
    if (savedTasks) this.tasks = savedTasks;
  },
  methods: {
    addTask(newTask) {
      this.tasks.push(newTask);
      this.saveTasks();
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

.container {
  max-width: 800px;
}
</style>
