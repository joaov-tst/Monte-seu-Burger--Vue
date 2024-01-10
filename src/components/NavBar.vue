<template>
<nav>
    <router-link to="/">
        <img :src="logo" :alt="alt" id="logo">
    </router-link>
    <div id="navegacao">
        <router-link to="/">Home</router-link> |
        <router-link to="/pedidos">Pedidos</router-link>
    </div>
</nav>

</template>

<script>
export default{
    name: "NavBar",
    props: ["logo", "alt"]
    

}

</script>

<style scoped>
    *{
        padding: 0px;
        margin: 0px;
        box-sizing: border-box;
    }
    nav{
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
        background-color: #1a1a1a;
        width: 100%;
        height: 12vh;
        padding: 10px 20px 10px 20px;
    }

    nav #logo{
        width: 25%;
    }

    nav a{
        color: white;
        text-decoration: none;
    }
    nav a:hover{
        color: #42b883;
    }
</style>
