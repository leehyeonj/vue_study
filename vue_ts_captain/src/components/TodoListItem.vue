<template>
  <li>
    <span class="item complete" @click="toggleItem">{{ todoItem }}</span>
    <button @click="removeItem">삭제</button>
  </li>
</template>
<script lang="ts">
import { Todo } from "@/App.vue";
import Vue, { PropType } from "vue";
export default Vue.extend({
  props: {
    todoItem: {
      type: Object as PropType<Todo>,
    },
    index: {
      type: Number,
    },
  },
  methods: {
    toggleItem() {
      this.$emit("toggle", this.todoItem, this.index);
    },
    removeItem() {
      this.$emit("remove", this.index);
    },
  },
});
</script>
<style scoped>
.item {
  cursor: pointer;
}
.complete {
  text-decoration: line-through;
}
</style>
