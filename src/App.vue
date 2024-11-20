<template>
  <div class="container">
    <br />
    <h1 class="title has-text-centered">To Do List</h1>

    <TaskForm @add-task="addTask" />
    <div class="box">
      <div class="field">
        <input 
          class="input" 
          type="text" 
          placeholder="Search tasks..." 
          v-model="searchQuery" 
        />
      </div>
      <div class="field">
        <div class="select">
          <select v-model="filterPriority">
            <option value="">All Priorities</option>
            <option value="Low">Low</option>
            <option value="Medium">Medium</option>
            <option value="High">High</option>
          </select>
        </div>
      </div>
    </div>
    <TaskList 
      :tasks="filteredTasks" 
      @delete-task="deleteTask" 
      @update-task="updateTask" 
      @toggle-completion="toggleCompletion" 
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
      searchQuery: '',
      filterPriority: '',
    };
  },
  computed: {
    filteredTasks() {
      return this.tasks.filter((task) => {
        const matchesSearch = task.title
          .toLowerCase()
          .includes(this.searchQuery.toLowerCase());
        const matchesPriority =
          !this.filterPriority || task.priority === this.filterPriority;
        return matchesSearch && matchesPriority;
      });
    },
  },
  created() {
    const savedTasks = JSON.parse(localStorage.getItem('tasks'));
    if (savedTasks) this.tasks = savedTasks;
  },
  methods: {
    addTask(newTask) {
      this.tasks.push({ ...newTask, completed: false });
      this.saveTasks();
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
      this.saveTasks();
    },
    updateTask() {
      this.saveTasks();
    },
    toggleCompletion(index) {
      this.tasks[index].completed = !this.tasks[index].completed;
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
