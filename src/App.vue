<template>
<NavHeader></NavHeader>
  <NavMain></NavMain>
  <NavFooter @addTodo="handleAddTodo" ></NavFooter>

</template>

<script>
import NavHeader from "@/components/NavHeader.vue";
// import NavFooter from "@/components/NavFooter.vue";



export default {
  name: 'App',
  components: {

    NavHeader
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
