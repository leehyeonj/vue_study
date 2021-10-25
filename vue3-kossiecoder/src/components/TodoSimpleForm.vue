<template>
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
</template>

<script>
import {ref} from 'vue';

export default {
    setup(props, context){
        const todo = ref('');
        const hasError = ref(false);
        const onSubmit = () =>{
            if(todo.value === ''){
                hasError.value = true
            }
            else{
                context.emit('add-todo', {
                    id: Date.now(),
                    subject : todo.value,
                    completed : false,
                });
                hasError.value = false;
                todo.value = '';
            }
        }

    return {
        todo, 
        hasError,
        onSubmit
    }
    }
}
</script>

<style lang="">
    
</style>