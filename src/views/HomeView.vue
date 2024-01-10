<template>
  <div class="main-content">
    <h1>HOME</h1>
    <BurgerForm />
  </div>
</template>

<script>
import BurgerForm from "../components/BurgerForm.vue"
export default{
  name: "HomeView",
  components:{
    BurgerForm
  }
}
</script>

<style>
    *{
        padding: 0px;
        margin: 0px;
        box-sizing: border-box;
    }
</style>
