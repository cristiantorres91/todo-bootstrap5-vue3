<template>
  <div class="input-group my-4">
    <input
      type="text"
      class="form-control"
      placeholder="run"
      v-model="task"
      @keyup.enter="addTask"
    />
    <button class="btn btn-secondary" type="button" @click="addTask">
      Add
    </button>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  name: "AddTask",

  emits: ["addTask"],
  setup(props, { emit }) {
    const task = ref('');

    const addTask = () => {
      const newTask = {
          name: task.value,
          done: false,
      }
      emit("addTask", newTask);
      task.value = "";
    };
    return {
        task,
        addTask,
    };
  },
};
</script>

<style lang="scss" scoped></style>
