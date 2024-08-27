<template>
    <div class="task-filter">
      <div class="filter-group">
        <label for="category-select">Category:</label>
        <select id="category-select" v-model="filter.category" @change="applyFilter">
          <option value="">All Categories</option>
          <option v-for="category in categories" :key="category" :value="category">
            {{ category }}
          </option>
        </select>
      </div>
      <div class="filter-group">
        <label>
          <input type="checkbox" v-model="filter.showCompleted" @change="applyFilter" />
          Show Completed
        </label>
      </div>
    </div>
</template>
  
<script>
  export default {
    data() {
      return {
        filter: {
          category: '',
          showCompleted: true,
        },
      };
    },
    props: {
      tasks: {
        type: Array,
        default: () => [],
      },
    },
    computed: {
      categories() {
        if (!this.tasks || !this.tasks.length) {
          return [];
        }
        const categories = this.tasks.map((task) => task.category || '');
        return [...new Set(categories.filter((category) => category))];
      },
    },
    methods: {
      applyFilter() {
        this.$emit('filterTasks', this.filter);
      },
    },
  };
</script>
  
<style scoped>
.task-filter {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 20px;
}
  
.filter-group {
    display: flex;
    align-items: center;
}
  
.filter-group label {
    margin-right: 10px;
    font-weight: bold;
}
  
#category-select {
    padding: 5px;
    border-radius: 4px;
    border: 1px solid #ccc;
}
  
input[type="checkbox"] {
    margin-right: 5px;
}
  
@media (max-width: 600px) {
    .task-filter {
      flex-direction: column;
      align-items: flex-start;
    }
  
    .filter-group {
      margin-bottom: 10px;
    }
}
</style>
  