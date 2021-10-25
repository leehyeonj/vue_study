<template>
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
</template>

<script>
export default {
   props : {
       todos: {
           type: Array,
           required : true
       }
   }
};
</script>

<style lang="scss" scoped>

</style>