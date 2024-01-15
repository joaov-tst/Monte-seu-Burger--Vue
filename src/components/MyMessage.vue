<template>
    <div id="msg-content" class="alert alert-success">
        <h5>{{ msg }}</h5>
    </div>
</template>

<script>
export default {
    name: "MyMessage",
    props:{msg: String}

}
</script>

<style scoped>
#msg-content{
    transition: 0.7s;
    border-radius: 5px;
    background-color: #42b883;
    padding: 5px;
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 10px;
}

#msg h5{
    margin: 0px;
    padding: 4px;
    font-weight: 500;
    line-height: 1;
    color: rgb(224, 243, 231);

}

</style>