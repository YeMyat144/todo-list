<template>
  <div v-if="tasks.length" class="box mt-4">
    <h2 class="subtitle" style="color: greenyellow;">Task List</h2>
    <div class="table-container">
      <table class="table is-fullwidth">
        <thead>
          <tr>
            <th>Title</th>
            <th>Category</th>
            <th>Due Date</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(task, index) in tasks" :key="index">
            <td>
              <input
                class="input is-small"
                v-model="task.title"
                @change="emitUpdate"
              />
            </td>
            <td>
              <input
                class="input is-small"
                v-model="task.category"
                @change="emitUpdate"
              />
            </td>
            <td>
              <input
                class="input is-small"
                type="date"
                v-model="task.date"
                @change="emitUpdate"
              />
            </td>
            <td>
              <button
                class="button is-danger is-small"
                @click="emitDelete(index)"
              >
                Delete
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
  <div v-else class="notification is-info">
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
  methods: {
    emitDelete(index) {
      this.$emit('delete-task', index);
    },
    emitUpdate() {
      this.$emit('update-task');
    },
  },
};
</script>
