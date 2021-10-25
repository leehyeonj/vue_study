<template>
  <div class="name">
    {{greeting(name)}}
  </div>
</template>

<script>
export default {
 setup(){
   const name = 'lee';

   const greeting = (name) =>{
     return 'hello' + name;
   }
   return{
     name,
     greeting
   }
 }
};
</script>

<style lang="scss" scoped>

</style>