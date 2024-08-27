<template>
  <div id="app" class="container">
    <h1>To-Do List</h1>
    <AddTask @addTask="addTask" />
    <TaskFilter @filterTasks="filterTasks" />
    <TaskList
      :tasks="filteredTasks"
      @deleteTask="deleteTask"
      @toggleComplete="toggleComplete"
      @editTask="editTask"
    />
  </div>
</template>

<script>
import AddTask from './components/AddTask.vue';
import TaskList from './components/TaskList.vue';
import TaskFilter from './components/TaskFilter.vue';

export default {
  name: 'App',
  components: {
    AddTask,
    TaskList,
    TaskFilter,
  },
  data() {
    return {
      tasks: JSON.parse(localStorage.getItem('tasks')) || [],
      filteredTasks: [],
    };
  },
  methods: {
    addTask(task) {
      this.tasks.push(task);
      this.saveTasks();
      this.filterTasks();
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
      this.saveTasks();
      this.filterTasks();
    },
    toggleComplete(index) {
      this.tasks[index].completed = !this.tasks[index].completed;
      this.saveTasks();
      this.filterTasks();
    },
    editTask({ index, newTask }) {
      this.tasks[index].name = newTask.name;
      this.tasks[index].category = newTask.category;
      this.tasks[index].dueDate = newTask.dueDate;
      this.saveTasks();
      this.filterTasks();
    },
    saveTasks() {
      localStorage.setItem('tasks', JSON.stringify(this.tasks));
    },
    filterTasks(filter = { category: '', showCompleted: true }) {
      this.filteredTasks = this.tasks.filter((task) => {
        const matchesCategory = filter.category
          ? task.category === filter.category
          : true;
        const matchesCompletion = filter.showCompleted
          ? true
          : !task.completed;
        return matchesCategory && matchesCompletion;
      });
    },
  },
  mounted() {
    this.filterTasks();
  },
};
</script>

<style scoped>
.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
}

h1 {
  text-align: center;
  margin-bottom: 20px;
}
</style>
