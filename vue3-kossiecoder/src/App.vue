<template>
  <div class="name">
    {{name}}
  </div>
  <button 
  class="btn btn-primary"
  v-on:click="updateName"
  >click</button>
</template>

<script>
import {ref} from 'vue'
export default {
 setup(){
   const name = ref('lee');

   const greeting = (name) =>{
     return 'hello' + name;
   }

   const updateName = ()=>{
    name.value = 'hyeonju'
   }
   return{
     name,
     greeting,
     updateName
   }
 }
};
</script>

<style lang="scss" scoped>

</style>