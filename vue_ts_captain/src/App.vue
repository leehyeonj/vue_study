<template>
  <div>
    <h1>Vue Todo with Typescript</h1>
    <TodoInput :item="todoText" @input="updatTodoText" @add="addTodoItem" />
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import TodoInput from "./components/TodoInput.vue";

export default Vue.extend({
  components: {
    TodoInput,
  },
  data() {
    return {
      todoText: "",
    };
  },
  methods: {
    updatTodoText(value: string) {
      this.todoText = value;
    },
    addTodoItem() {
      const value = this.todoText;
      localStorage.setItem(value, value);
      this.initTodoText();
    },
    initTodoText() {
      this.todoText = "";
    },
  },
});
</script>
