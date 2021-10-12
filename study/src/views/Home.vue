<template>
  <div>
    <h1>This is homepage</h1>
    <p>{{ name }}</p>

    <Little title="home title"/>
  </div>
</template>

<script>
import Little from "@/components/Little.vue";
export default {
  components : {
    Little
  },

  data(){
    return {
      name: "현주"
    }
  }

}
</script>

<style scoped>
h1{
  color: red;
}
</style>