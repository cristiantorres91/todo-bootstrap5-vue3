<template>
<div v-for="(item, index) in tasks" :key="index">
<div :class="['alert' ,  item.done ? 'alert-success' : 'alert-danger'] " role="alert" >
  <div class="d-flex justify-content-between align-items-center">
    <div>
       <h5>{{item.name}}</h5>
    </div>
    <div >
      <button type="button" class="btn btn-outline-success bt-sm mx-3" @click="editTask(index)"><i class="bi bi-check-lg"></i></button>
      <button type="button" class="btn btn-outline-danger bt-sm" @click="deleteTask(index)"><i class="bi bi-x-lg"></i></button>
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
  
  emits: ['editTask', 'deletTask'],
    setup (props, {emit}) {

      const editTask = (index) =>{
        emit('editTask', index);
      } 

      const deleteTask = (index) =>{
        emit('deleteTask', index);
      } 
        return {
          editTask,
          deleteTask
        }
    }
}
</script>

<style lang="scss" scoped>

</style>