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
        //Dados que serão passados como props no Navbar
        logo_src: "/img/logo.png",
        logo_alt: "Logo Vue"
      }
    }
  }
</script>

<style>

*{
  padding: 0px;
  margin: 0px;
  box-sizing: border-box;
  transition: 0.5s;
}
  .main-content{
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      padding: 20px;
      width: 100%;
      min-height: 70vh;
      background-color: rgb(238, 248, 242);
  }
  h1{
    color:#1a1a1a;
  }
</style>

