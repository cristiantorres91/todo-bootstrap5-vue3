<template>
  <div class="container" v-if="tasks.length > 0">
    <div class="row">
      <div class="col bg-danger text-white">
        Pending : {{tasks.filter(t => t.done == false).length}}
      </div>
      <div class="col bg-success text-white">
        Completed : {{tasks.filter(t => t.done == true).length}}
      </div>
    </div>
  </div>
  <div v-for="(item, index) in tasks" :key="index" class="pt-2">
    <div
      :class="['alert', item.done ? 'alert-success' : 'alert-danger']"
      role="alert"
    >
      <div class="d-flex justify-content-between align-items-center">
        <div>
          <h5>{{ item.name }}</h5>
        </div>
        <div>
          <button
            type="button"
            class="btn btn-outline-success bt-sm mx-3"
            @click="editTask(index)"
          >
            <i class="bi bi-check-lg"></i>
          </button>
          <button
            type="button"
            class="btn btn-outline-danger bt-sm"
            @click="deleteTask(index)"
          >
            <i class="bi bi-x-lg"></i>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Tasks",
  props: {
    tasks: {
      type: Array,
      default: () => [],
    },
  },

  emits: ["editTask", "deleteTask"],
  setup(props, { emit }) {
    const editTask = (index) => {
      emit("editTask", index);
    };

    const deleteTask = (index) => {
      emit("deleteTask", index);
    };
    return {
      editTask,
      deleteTask,
    };
  },
};
</script>

<style lang="scss" scoped></style>
