<template>
<div>
  <NavBar :logo ="logo_src" :alt="logo_alt"/>
  <router-view/>
  <MyFooter />
</div>
</template>
<script>
import NavBar from "./components/NavBar"
import MyFooter from "./components/MyFooter"

  export default{
    components:{
      NavBar,
      MyFooter
    },
    data(){
      return{
        logo_src: "/img/logo.png",
        logo_alt: "Logo Vue"
      }
    }
  }
</script>

<style>
  .main-content{
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      padding: 20px;
      width: 100%;
      min-height: 70vh;
      background-color: rgb(224, 243, 231);
  }
</style>

