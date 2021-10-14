<template>
  <div>
    Count : {{ count }}, double : {{ double }} <br>
    <button @click="increment">Increase</button>
    <Triple/>
  </div>
</template>

<script>
import Triple from "./components/Triple.vue";

export default {
  components : {
    Triple
  },
  data(){
    return {
      count: 0,
    }
  },
  computed : {
    double(){
      return this.count * 2;
    }
  },
  methods : {
    increment(){
      this.count++;
    }
  }
}
</script>
