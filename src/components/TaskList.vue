<template>
  <div v-if="tasks.length" class="box mt-4">
    <h2 class="subtitle" style="color: greenyellow;">Task List</h2>
    <div class="table-container">
      <table class="table is-fullwidth">
        <thead>
          <tr>
            <th>Title</th>
            <th>Category</th>
            <th>Priority</th>
            <th>Due Date</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(task, index) in tasks" :key="index">
            <td :class="{ 'has-text-grey-light': task.completed }">
              {{ task.title }}
            </td>
            <td :class="{ 'has-text-grey-light': task.completed }">
              {{ task.category }}
            </td>
            <td :class="{ 'has-text-grey-light': task.completed }">
              <span
                class="tag"
                :class="{
                  'is-success': task.priority === 'Low',
                  'is-warning': task.priority === 'Medium',
                  'is-danger': task.priority === 'High',
                }"
              >
                {{ task.priority }}
              </span>
            </td>
            <td :class="{ 'has-text-grey-light': task.completed }">
              {{ task.date }}
            </td>
            <td>
              <button
                class="button is-danger is-small"
                @click="$emit('delete-task', index)"
              >
                Delete
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
  <div v-else >
    No tasks available. Add a new task to get started!
  </div>
</template>

<script>
export default {
  props: {
    tasks: {
      type: Array,
      required: true,
    },
  },
};
</script>
