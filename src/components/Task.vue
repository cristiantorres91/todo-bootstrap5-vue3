<template>
<div v-for="(item, index) in tasks" :key="index">
<div :class="['alert' , 'alert-danger'] " role="alert" >
  <div class="d-flex justify-content-between align-items-center">
    <div>
       <h5>{{index}} {{item.name}} {{item.done}}</h5>
    </div>
    <div >
      <button type="button" class="btn btn-outline-success bt-sm mx-3" @click="editTask"><i class="bi bi-check-lg"></i></button>
      <button type="button" class="btn btn-outline-danger bt-sm"><i class="bi bi-x-lg"></i></button>
    </div>
  </div>
</div>
</div>
</template>

<script>

export default {
  props: {
    tasks: {
      type: Array,
      default: () => [],
    },
  },
  
  emits: ['editTask'],
    setup (props, { emit }) {
      const editTask = () =>{
        emit('editTask');
      } 
        return {
          editTask
        }
    }
}
</script>

<style lang="scss" scoped>

</style>