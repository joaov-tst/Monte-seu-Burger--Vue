<template>
    <div>
        <h5>Monte seu Burger!</h5>
        <form id="burger-form">
            <div id="inputs-container">
                <label for="name">Informe seu nome:</label> <br>
                <input type="text" name="name" id="name" class="input-large" v-model="nome" placeholder="Digite seu nome..."> <br>

                <label for="paes">Opções de pão:</label> <br>
                <select name="paes" id="paes" v-model="pao">
                    <option value="">Escolha seu pão</option>
                    <option v-for="pao in paes" :key="pao.id" :value="pao.id">{{pao.tipo}}</option>
                </select> <br>
                <label for="paes">Opções de carne:</label> <br>
                <select name="carnes" id="carnes" v-model="carne">
                    <option value="">Escolha sua carne</option>
                    <option v-for="carne in carnes" :key="carne.id" :value="carne.id">{{carne.tipo}}</option>
                </select>
                <div id="input-container">
                    <label for="opcionais">Escolha seus opcionais:</label> <br>
                    <div id="all-check">
                        <div id="checkbox-container" v-for="opcao in opcionaisdata" :key="opcao.id">
                            <input type="checkbox" :value="opcao.tipo" name="opcionais" v-model="opcionais"> <span>{{opcao.tipo}}</span>
                        </div>
                    </div>
                </div>
                <input type="submit" class="btn btn-primary input-large" value="Fazer pedido!">

            </div>
        </form>

    </div>

    
</template>

<script>
export default{
    name: "BurgerForm",
    data(){
        return{
            //Opções resgatadas do db.json
            paes: null,
            carnes: null,
            opcionaisdata: null,

            //Dados informados pelo usuário
            pao: null,
            carne: null,
            opcionais: [],
            nome: null,
            status: "Solicitado",
            msg: null
        }
    },

    methods:{
        async getIngredientes(){
            const request = await fetch("http://localhost:3000/ingredientes");
            const data = await request.json();
            this.paes = data.paes
            this.carnes = data.carnes
            this.opcionaisdata = data.opcionais
        }
    },

    mounted(){
        this.getIngredientes()
    }
}
</script>

<style scoped>
#burger-form{
    display: flex;
    justify-content: center;
    align-items: center;
    width: 40vw;
    padding: 20px;
    background-color: transparent;
    border-radius:20px;
    box-shadow: 0px 0px 3px gray;
}

#burger-form label{
    font-weight: 500;
    font-size: 20px;
}

#burger-form #inputs-container{
    width: 70%;
}
#inputs-container .input-large, select{
    width: 100%;
}

#all-check{
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
    align-items: center;
    justify-content: center;
}
</style>