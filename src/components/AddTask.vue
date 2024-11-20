<template>
  <div class="add-task">
    <input 
      v-model="newTask" 
      type="text" 
      placeholder="Add a new task"
      @keyup.enter="addTask"
    />
    <button @click="addTask">Add</button>
  </div>
</template>

<script>
export default {
  props: ['onAdd'],
  data() {
    return {
      newTask: '',
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim()) {
        this.onAdd(this.newTask.trim());
        this.newTask = '';
      }
    },
  },
};
</script>

<style scoped>
.add-task {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}
</style>
