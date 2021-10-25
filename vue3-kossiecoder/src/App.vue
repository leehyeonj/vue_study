<template>
<div class="container">
  <h1>TO DO LIST</h1>
   <input 
        class="form-control"
        type="text" 
        v-model="searchText"
        placeholder="search"
        >
  <TodoSimpleForm @add-todo = "addTodo"/>
  <div style="color: red">{{error}}</div>
  <div v-if="!filteredTodos.length">
    There is nothing to display
  </div>
  <TodoList 
  :todos="filteredTodos" 
  @toggle-todo="toggleTodo" 
  @delete-todo="deleteTodo"
  />
</div>

</template>

<script>
import {ref, computed} from 'vue'
import TodoSimpleForm from "./components/TodoSimpleForm.vue";
import TodoList from "./components/TodoList.vue";
import axios from "axios";


export default {
  components : {
    TodoSimpleForm,
    TodoList
  },

 setup(){
   const todos = ref([]);
   const error = ref('');
   const todoStyle = {
     textDecoration: 'line-through',
     color: 'gray'
   }
 
   const addTodo = (todo)=>{
     //디비에 저장
     axios.post('http://localhost:3000/todos', {
       subject : todo.subject,
       completed : todo.completed
     }).then(res => {
       todos.value.push(res.data)
       console.log(res)
     }).catch(err => {
       console.log(err)
       error.value = "Somethins went wrong";
     })
     
 
   }

   const deleteTodo = (index) =>{
     todos.value.splice(index, 1)
   }

   const toggleTodo = (index) =>{
      todos.value[index].completed = !todos.value[index].completed
   }

   const searchText = ref('');
   const filteredTodos = computed (() => {
     if(searchText.value){
       return todos.value.filter(todo => {
         return todo.subject.includes(searchText.value)
       });
     }
     return todos.value;
   })

   return{

     todos,
     error,
     addTodo,
     todoStyle,
     deleteTodo,
     toggleTodo,
     searchText,
     filteredTodos
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