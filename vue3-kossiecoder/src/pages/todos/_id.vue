<template>
  <h1>To-Do Page</h1>
  <div v-if="loading">Loading..</div>
  <form v-else @submit.prevent="onSave">
    <div class="row">
      <div class="col-6">
        <div class="form-group">
          <label>Subject</label>
          <input v-model="todo.subject" type="text" class="form-control" />
        </div>
      </div>
      <div class="col-6">
        <div class="form-group">
          <label>Status</label>
          <div>
            <button
              class="btn"
              type="button"
              :class="todo.completed ? 'btn-success' : 'btn-danger'"
              @click="toggleTodoStatus"
            >
              {{ todo.completed ? "Completed" : "Incomplete" }}
            </button>
          </div>
        </div>
      </div>
    </div>

    <button type="submit" class="btn btn-primary mt-2" :disabled="!todoUpdated">
      Save
    </button>
    <button class="btn btn-outline-dark ml-2 mt-2" @click="moveToTodoListPage">
      Cancel
    </button>
  </form>
  <Toast v-if="showToast" :message="toastMessage" :type="toastAlertType" />
</template>


<script>
import { useRoute, useRouter } from "vue-router";
import axios from "axios";
import { ref, computed } from "@vue/reactivity";
import _ from "lodash";
import Toast from "../../components/Toast.vue";

export default {
  components: {
    Toast,
  },

  setup() {
    const route = useRoute(); //params id 가져오기
    const router = useRouter();
    const todo = ref(null);
    const originalTodo = ref(null);
    const loading = ref(true);
    const showToast = ref(true);
    const toastMessage = ref("");
    const toastAlertType = ref("");
    const todoId = route.params.id;

    //한개의 todo 데이터 가져오기
    const getTodo = async () => {
      try {
        const res = await axios.get("http://localhost:3000/todos/" + todoId);
        originalTodo.value = { ...res.data };
        todo.value = { ...res.data };
        loading.value = false;
      } catch (err) {
        triggerToast("something went wrong!", "danger");
      }
    };

    //바뀐 내용이 없으면 save 버튼을 disable 로 바꾸겠다.
    const todoUpdated = computed(() => {
      return !_.isEqual(todo.value, originalTodo.value);
    });

    //상세 페이지에서 토글하기
    const toggleTodoStatus = () => {
      todo.value.completed = !todo.value.completed;
    };

    //리스트 페이지로 이동하기
    const moveToTodoListPage = () => {
      router.push({
        name: "Todos",
      });
    };

    const triggerToast = (message, type = "success") => {
      toastMessage.value = message;
      toastAlertType.value = type;
      showToast.value = true;
      setTimeout(() => {
        toastMessage.value = "";
        showToast.value = false;
      }, 1000);
    };
    //저장하기
    const onSave = async () => {
      try {
        const res = await axios.put(`http://localhost:3000/todos/${todoId}`, {
          subject: todo.value.subject,
          completed: todo.value.completed,
        });
        originalTodo.value = { ...res.data };
        triggerToast("successfully saved!");
      } catch (err) {
        triggerToast("something went wrong!", "danger");
      }
    };
    getTodo();

    //return
    return {
      todo,
      loading,
      toggleTodoStatus,
      moveToTodoListPage,
      onSave,
      todoUpdated,
      showToast,
      toastMessage,
      toastAlertType,
    };
  },
};
</script>

<style>
</style>