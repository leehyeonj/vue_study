<template>
  <div>
    <form v-on:submit.prevent="submitForm">
      <div>
        <label for="username">Id:</label>
        <input id="username" type="text" v-model="username">
      </div>
      <div>
        <label for="password">pw: </label>
        <input id="password" type="password" v-model="password">
      </div>
      <button type="submit">로그인</button>
    </form>
    <p v-if="isError">올바르지 않은 id입니다.</p>
  </div>
</template>

<script>
export default {
  data(){
    return {
      username : "",
      password : "",
      isError : false,
    }
  },
  methods : {
    submitForm() {
      console.log('submitted')
      this.isError = true;
      this.initForm()
    },
    initForm() {
      this.username = '';
      this.password = '';
    }
  }
}
</script>

<style>

</style>