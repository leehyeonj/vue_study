<template>
  <div>
    <form v-on:submit.prevent="submitForm">
      <div>
        <label for="username">Id:</label>
        <input id="username" type="text" v-model="username" 
        class="username-input"
        v-bind:class ="{'error' : isError}"
        >
      </div>
      <div>
        <label for="password">pw: </label>
        <input id="password" type="password" v-model="password">
      </div>
      <button v-bind:disabled="!isUsernameValid" type="submit">로그인</button>
    </form>
    <p v-if="isError">올바르지 않은 id입니다.</p>
    <p v-if="isUsernameValid">아이디가 이메일 형식이 맞습니다. </p>
  </div>
</template>

<script>
//이메일 형식 체크 함수
function validateEmail(email) {
    const re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
    return re.test(String(email).toLowerCase());
}

export default {
  data(){
    return {
      username : "",
      password : "",
      isError : false,
    }
  },
  //변화되었을 때 자동으로 계산
  computed: {
    isUsernameValid(){  
      return validateEmail(this.username)

    }
  },
  methods : {
    submitForm() {
      console.log('submitted')
      this.isError = true;
      // this.initForm()
    },
    initForm() {
      this.username = '';
      this.password = '';
    }
  }
}
</script>

<style scoped>
/* 현재 컴포넌트에만 적용되는 scoped */
.username-input {
  outline: none;
}
.username-input.error {
  border: 1px solid red;
}
</style>