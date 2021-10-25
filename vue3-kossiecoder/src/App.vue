<template>
<div class="container">
  <h1>TO DO LIST</h1>
  <form @submit.prevent="onSubmit" >
  <div  class="d-flex">
    <div class="flex-grow-1 mr-2">
        <input 
        class="form-control"
        type="text" 
        v-model="todo"
        placeholder="type new todo"
        >
    </div>
      <div>
        <button 
        class="btn btn-primary"
        type="submit"
        >add
        </button>
      </div>
  </div>
    <div v-show="hasError" style="color:red">아무것도 적지 않았군</div>
  </form>
  <div 
  class="card mt-2" 
  v-for="todo in todos" 
  :key="todo.id">

    <div class="card-body p-2">
      <div class="form-check">
        <input type="checkbox"
        class="form-check-input"
        v-model="todo.completed"
        >
        <label class="form-check-label">
          {{ todo.subject}}
        </label>
      </div>
      
    </div>
  </div>
</div>

</template>

<script>
import {ref} from 'vue'
export default {
 setup(){
   const todo = ref('');
   const todos = ref([ ]);
   const hasError = ref(false);
 
   const onSubmit = (e)=>{
     if(todo.value === ''){
       hasError.value = true;
     }
     else{
        e.preventDefault();
        todos.value.push({
          id: Date.now(),
          subject : todo.value,
          completed : false
        })
        hasError.value = false;
        todo.value = ''
     }
 
   }
   return{
     todo,
     todos,
     onSubmit,
     hasError
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