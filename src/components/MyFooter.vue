<template>
    <router-link to="/">
        <div id="footer-container">
            <a href="">LinkedIn</a> <br>
            <a href="">Github</a> <br>
            <a href="">Instagram</a><br>
        </div>
    </router-link>
</template>

<script>
export default {
    name: "MyFooter"
}
</script>

<style scoped>
    #footer-container{
        width: 100%;
        height: 18vh;
        background-color: #42b883;
    }
    #footer-container a{
        text-decoration: none;
        color: #1a1a1a;
        font-weight: 500;
    }
</style>