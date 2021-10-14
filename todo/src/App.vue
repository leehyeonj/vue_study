<template>
  <div>
    Count : {{ count }}, double : {{ double }} <br>
    <button @click="increment">Increase</button>
  </div>
</template>

<script>
export default {
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
