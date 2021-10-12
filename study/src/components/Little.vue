<template>
    <div>
        <h1>{{title}}</h1>
        <p>{{name}}</p>    
        <button @click="updateName">click</button>
    </div>
</template>

<script>
export default {
    props: {
        title : {
            type: String,
            required : true,
        }
    },
  data(){
    return {
      name: "현주"
    }
  },
   methods : {
       updateName(){
           this.name = "현주의 이름입니다."
       }
   }
}
</script>

<style scoped>

</style>