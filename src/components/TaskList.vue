<template>
    <div class="task-list">
      <div
        v-for="(task, index) in tasks"
        :key="index"
        class="task"
        :class="{ completed: task.completed }"
      >
        <div>
          <input
            type="checkbox"
            v-model="task.completed"
            @change="toggleComplete(index)"
          />
          <span>{{ task.name }}</span>
          <span class="category">[{{ task.category }}]</span>
          <span class="due-date">Due: {{ task.dueDate }}</span>
        </div>
        <div>
          <button @click="editTask(index)">Edit</button>
          <button @click="deleteTask(index)">Delete</button>
        </div>
      </div>
    </div>
</template>
  
<script>
  export default {
    props: {
      tasks: Array,
    },
    methods: {
      deleteTask(index) {
        this.$emit('deleteTask', index);
      },
      toggleComplete(index) {
        this.$emit('toggleComplete', index);
      },
      editTask(index) {
        const newTask = prompt('Edit task:', this.tasks[index].name);
        const newCategory = prompt(
          'Edit category:',
          this.tasks[index].category
        );
        const newDueDate = prompt('Edit due date:', this.tasks[index].dueDate);
        if (newTask) {
          this.$emit('editTask', {
            index,
            newTask: {
              name: newTask,
              category: newCategory,
              dueDate: newDueDate,
            },
          });
        }
      },
    },
  };
</script>
  
<style scoped>
.task-list {
    list-style-type: none;
    padding: 0;
}
  
.task {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px;
    border-bottom: 1px solid #ccc;
}
  
.task.completed span {
    text-decoration: line-through;
}
  
button {
    margin-left: 10px;
}
  
.category {
    margin-left: 10px;
    font-style: italic;
}
  
.due-date {
    margin-left: 10px;
    color: #007bff;
}
</style>
  