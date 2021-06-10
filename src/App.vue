<template>
  <Header />
<div class="container">
<div class="input-group my-4">
  <input type="text" class="form-control" placeholder="Runner" v-model="newTask" @keyup.enter="addTask" >
  <button class="btn btn-secondary" type="button" @click="addTask" >Add</button>
</div>
  <Task :tasks="tasks" @editTask="editTask"/>
</div>
</template>

<script>
import Header from './components/Header.vue';
import Task from '@/components/Task.vue';
import { ref } from "vue";


export default {
  name: 'App',
  components: {
    Header,
    Task
  },

  setup() {
    const newTask = ref('');
    const tasks = ref([]);

    const addTask = () => {
      tasks.value.push(
        {
          name: newTask.value,
          done: false,
        }
      );
      console.log(tasks.value);
      newTask.value = "";
    };

    const editTask = () =>{
      console.log('edit');
    };

    return {
      newTask,
      tasks,
      addTask,
      editTask
    };
  },
}
</script>

<style>

</style>
