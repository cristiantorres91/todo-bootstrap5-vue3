<template>
  <h4 className="bg-primary text-white text-center p-4">
    Todo App - {{name}}
  </h4>
</template>

<script>
import { onMounted, ref } from "vue";

export default {
  name: "Header",
  setup() {
    const  name = ref('');
    onMounted(() => {
      const person = prompt("Please enter your name:");
      if (person == null || person == "") {
        name.value = "Leo Messi";
      } else {
        name.value =  person ;
      }
    });
    return {
      name
    };
  },
};
</script>

<style lang="scss" scoped></style>
