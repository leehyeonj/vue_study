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
    v-for="(todo,index) in todos" 
    :key="todo.id">

    <div class="card-body p-2 d-flex align-items-center">
      <div class="form-check flex-grow-1">
        <input type="checkbox"
        class="form-check-input"
        v-model="todo.completed"
        >
        <label class="form-check-label"
        :class="{todo: todo.completed}"
        >
          {{ todo.subject}}
        </label>
      </div>
      <div>
        <button 
        class="btn btn-danger btn-sm"
        @click="deleteTodo(index)"
        >delete</button>
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
   const todoStyle = {
     textDecoration: 'line-through',
     color: 'gray'
   }
 
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

   const deleteTodo = (index) =>{
     todos.value.splice(index, 1)
   }
   return{
     todo,
     todos,
     onSubmit,
     hasError,
     todoStyle,
     deleteTodo
   }
 }
};
</script>

<style>
.todo {
  color: gray;
  text-decoration: line-through;
}

</style>