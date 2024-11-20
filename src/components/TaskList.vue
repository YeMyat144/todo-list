<template>
  <ul class="task-list">
    <li v-for="task in filteredTasks" :key="task.id">
      <input 
        type="checkbox" 
        :checked="task.completed"
        @change="toggleTask(task.id)"
      />
      <span :class="{ completed: task.completed }">{{ task.text }}</span>
      <button @click="removeTask(task.id)">Delete</button>
    </li>
  </ul>
</template>

<script>
export default {
  props: ['tasks', 'filter', 'onToggle', 'onRemove'],
  computed: {
    filteredTasks() {
      if (this.filter === 'active') {
        return this.tasks.filter(task => !task.completed);
      }
      if (this.filter === 'completed') {
        return this.tasks.filter(task => task.completed);
      }
      return this.tasks;
    },
  },
  methods: {
    toggleTask(id) {
      this.onToggle(id);
    },
    removeTask(id) {
      this.onRemove(id);
    },
  },
};
</script>

<style scoped>
.task-list {
  list-style: none;
  padding: 0;
}
.completed {
  text-decoration: line-through;
}
</style>
