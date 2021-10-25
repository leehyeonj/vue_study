<template>
  <div v-bind:class="nameClass">
    {{name}}
  </div>
  <input type="text" v-bind:value="name">
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
   const nameClass = ref('name')

   const greeting = (name) =>{
     return 'hello' + name;
   }

   const updateName = ()=>{
    name.value = 'hyeonju'
    nameClass.value = 'green'
   }
   return{
     name,
     greeting,
     updateName,
     nameClass
   }
 }
};
</script>

<style>
.name {
  color: red;
}
.green{
  color : green;
}

</style>