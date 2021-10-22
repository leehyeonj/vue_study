<template>
  <div id="app">
    <h2>클릭하면 카운터가 올라갑니다.</h2>
    <p>{{count}} 회</p>
    <button v-on:click="countUp">카운터</button>
  </div>
</template>

<script>
export default {
  name: 'VueStudyHelloworld',
  el: "#app",
  data() {
    return {
      count : 0
    };
  },

  mounted() {
    
  },

  methods: {
    countUp() {
      this.count ++;
    }
  },
};
</script>

<style lang="scss" scoped>

</style>