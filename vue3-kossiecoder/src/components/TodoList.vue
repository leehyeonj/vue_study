<template>
  <div v-for="(todo, index) in todos" :key="todo.id" class="card mt-2">
    <div
      @click.stop="moveToPage(todo.id)"
      class="card-body p-2 d-flex align-items-center"
    >
      <div class="form-check flex-grow-1">
        <input
          class="form-check-input"
          type="checkbox"
          :checked="todo.completed"
          @change="toggleTodo(index, $event)"
          @click.stop
        />
        <label class="form-check-label" :class="{ todo: todo.completed }">
          {{ todo.subject }}
        </label>
      </div>
      <div>
        <button class="btn btn-danger btn-sm" @click.stop="deleteTodo(index)">
          Delete
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import { useRouter } from "vue-router";

export default {
  props: {
    todos: {
      type: Array,
      required: true,
    },
  },
  emits: ["toggle-todo", "delete-todo"],
  setup(props, { emit }) {
    const router = useRouter();

    //complete toggle
    const toggleTodo = (index, event) => {
      emit("toggle-todo", index, event.target.checked);
    };

    //delete
    const deleteTodo = (index) => {
      emit("delete-todo", index);
    };

    //page move
    const moveToPage = (todoId) => {
      console.log(todoId);
      // router.push("/todos/" + todoId);
      //장점 : 앱이 커지면 커질 수록 이 로직을 여러 군데에서 사용한다고 하면 path정보가 바뀌면 일일이 바꾸어주지 않아도 된다 .
      router.push({
        name: "Todo",
        params: {
          id: todoId,
        },
      });
    };
    return {
      toggleTodo,
      deleteTodo,
      moveToPage,
    };
  },
};
</script>

<style>
</style>