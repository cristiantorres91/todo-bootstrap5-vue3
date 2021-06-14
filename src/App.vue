<template>
  <Header />
<div class="container">
<!-- <div class="input-group my-4">
  <input type="text" class="form-control" placeholder="Runner" v-model="newTask" @keyup.enter="addTask" >
  <button class="btn btn-secondary" type="button" @click="addTask" >Add</button>
</div> -->
<AddTask @addTask="addTask"/>
  <Tasks :tasks="tasks" @editTask="editTask" @deleteTask="deleteTask"/>
</div>
</template>

<script>
import Header from '@/components/Header.vue';
import Tasks from '@/components/Tasks.vue';
import AddTask from '@/components/AddTask.vue';
import { onMounted, ref } from "vue";



export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask,
  },

  setup() {
    const tasks = ref([]);

      onMounted (() =>{
        let dataLocalStorage = JSON.parse(localStorage.getItem('tasks'))
        if(dataLocalStorage === null){
          tasks.value = [];
        }else{
          tasks.value = dataLocalStorage;
        }

      });

    const addTask = (task) => {
      tasks.value.push(
        {
          name: task.name,
          done: task.done,
        }
      );
      console.log(tasks.value);
      localStorage.setItem("tasks", JSON.stringify(tasks.value));
    };

    const editTask = (index) =>{
      tasks.value[index].done = true;
      localStorage.setItem("tasks", JSON.stringify(tasks.value));
    };

    const deleteTask = (index) => {
      tasks.value.splice(index, 1);
      localStorage.setItem("tasks", JSON.stringify(tasks.value));
    };

    return {
      tasks,
      addTask,
      editTask,
      deleteTask
    };
  },
}
</script>

<style>

</style>
