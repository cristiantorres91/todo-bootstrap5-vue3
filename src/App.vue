<template>
  <Header />
<div class="container">
<div class="input-group my-4">
  <input type="text" class="form-control" placeholder="Runner" v-model="newTask" @keyup.enter="addTask" >
  <button class="btn btn-secondary" type="button" @click="addTask" >Add</button>
</div>
  <Task :tasks="tasks" @editTask="editTask($event,index)" @deleteTask="deleteTask($event, index)"/>
</div>
</template>

<script>
import Header from './components/Header.vue';
import Task from '@/components/Task.vue';
import { onMounted, ref } from "vue";



export default {
  name: 'App',
  components: {
    Header,
    Task
  },

  setup() {
    const newTask = ref('');
    const tasks = ref([]);

      onMounted (() =>{
        let dataLocalStorage = JSON.parse(localStorage.getItem('tasks'))
        console.log(dataLocalStorage);
        if(dataLocalStorage === null){
          tasks.value = [];
        }else{
          tasks.value = dataLocalStorage;
        }

      });

    const addTask = () => {
      tasks.value.push(
        {
          name: newTask.value,
          done: false,
        }
      );
      console.log(tasks.value);
      newTask.value = "";
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
      newTask,
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
