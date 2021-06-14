<template>
  <Header />
  <div class="container">
    <AddTask @addTask="addTask" />
    <Tasks :tasks="tasks" @editTask="editTask" @deleteTask="deleteTask" />
  </div>
</template>

<script>
import Header from "@/components/Header.vue";
import Tasks from "@/components/Tasks.vue";
import AddTask from "@/components/AddTask.vue";
import { onMounted, ref } from "vue";

export default {
  name: "App",
  components: {
    Header,
    Tasks,
    AddTask,
  },

  setup() {
    const tasks = ref([]);

    onMounted(() => {
      let dataLocalStorage = JSON.parse(localStorage.getItem("tasks"));
      if (dataLocalStorage === null) {
        tasks.value = [];
      } else {
        tasks.value = dataLocalStorage;
      }
    });

    const updateLocalStorage = () => {
      localStorage.setItem("tasks", JSON.stringify(tasks.value));
    };

    const addTask = (task) => {
      tasks.value.push({
        name: task.name,
        done: task.done,
      });
      console.log(tasks.value);
      updateLocalStorage();
    };

    const editTask = (index) => {
      tasks.value[index].done = true;
      updateLocalStorage();
    };

    const deleteTask = (index) => {
      tasks.value.splice(index, 1);
      updateLocalStorage();
    };

    return {
      updateLocalStorage,
      tasks,
      addTask,
      editTask,
      deleteTask,
    };
  },
};
</script>

<style></style>
