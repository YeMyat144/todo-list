<template>
  <div class="task-filter">
    <button 
      v-for="option in filterOptions" 
      :key="option.value" 
      :class="{ active: option.value === currentFilter }"
      @click="updateFilter(option.value)"
    >
      {{ option.label }}
    </button>
  </div>
</template>

<script>
export default {
  props: ['currentFilter', 'onFilterChange'],
  data() {
    return {
      filterOptions: [
        { label: 'All', value: 'all' },
        { label: 'Active', value: 'active' },
        { label: 'Completed', value: 'completed' },
      ],
    };
  },
  methods: {
    updateFilter(filter) {
      this.onFilterChange(filter);
    },
  },
};
</script>

<style scoped>
.task-filter button {
  margin: 0 5px;
}
button.active {
  font-weight: bold;
}
</style>
