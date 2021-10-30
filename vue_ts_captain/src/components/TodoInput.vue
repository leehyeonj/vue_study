<template>
  <div>
    <label for="todo-input">오늘 할 일</label>
    <input id="todo-input" type="text" :value="item" @input="handleInput" />
    <button @click="addTodo" type="button">add</button>
  </div>
</template>

<script>
import Vue from "vue";
export default Vue.extend({
  props: ["item"],
  components: {},
  methods: {
    handleInput(event) {
      //   event.target.value;
      this.$emit("input", event.target.value);
    },
    addTodo() {
      this.$emit("add");
    },
  },
});
</script>
