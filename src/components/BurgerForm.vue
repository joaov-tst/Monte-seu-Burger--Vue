<template>
    <div>
        <MyMessage :msg="msg" v-show="msg"/>
        <form id="burger-form" @submit="createBurger">
            <h2>MONTE SEU <span>BURGER</span></h2>
            <div id="inputs-container">
                <label for="name">Informe seu nome:</label> <br>
                <input type="text" name="name" id="name" class="input-large" v-model="nome" placeholder="Digite seu nome..."> <br>

                <label for="paes">Opções de pão:</label> <br>
                <select name="paes" id="paes" v-model="pao">
                    <option value="">Escolha seu pão</option>
                    <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">{{pao.tipo}}</option>
                </select> <br>
                <label for="paes">Opções de carne:</label> <br>
                <select name="carnes" id="carnes" v-model="carne">
                    <option value="">Escolha sua carne</option>
                    <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">{{carne.tipo}}</option>
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
import MyMessage from './MyMessage.vue';

export default{
    name: "BurgerForm",
    data() {
        return {
            //Opções resgatadas do db.json
            paes: null,
            carnes: null,
            opcionaisdata: null,
            //Dados informados pelo usuário
            nome: null,
            carne: null,
            pao: null,
            opcionais: [],
            status: "Solicitado",
            msg: null
        };
    },
    methods: {
        //Requisição apra puxar as opções
        async getIngredientes() {
            const request = await fetch("http://localhost:3000/ingredientes");
            const data = await request.json();
            this.paes = data.paes;
            this.carnes = data.carnes;
            this.opcionaisdata = data.opcionais;
        },

        //Requisição POST enviando o pedido
        async createBurger(e) {
            e.preventDefault(); // Desabilitando o evento padrão do submit que é reload da página
            //Objeto que será enviado na requisição POST
            const data = {
                nome: this.nome,
                carne: this.carne,
                pao: this.pao,
                opcionais: Array.from(this.opcionais), //Enviando o array inteiro na requisição
                status: "Solicitado"
            };
            const dataJson = JSON.stringify(data); // Convertendo o objeto para texto antes da requisição
            const request = await fetch("http://localhost:3000/burgers", {
                method: "POST",
                body: dataJson,
                headers: {
                    "Content-Type": "application/json"
                }
            });
            const res = await request.json();

            //Notificando o usuário
            this.msg = `Pedido realizado com sucesso! Id do pedido: #${res.id}`

            setTimeout(()=> this.msg = "", 5000)
            //Limpando campos
            this.nome = "";
            this.carne = "";
            this.pao = "";
            this.opcionais = [];
        }
    },
    mounted() {
        this.getIngredientes();
    },
    components: { MyMessage }
}
</script>

<style scoped>
#burger-form{
    display: flex;
    justify-content: center;
    align-items: center;
    width: 50vw;
    padding: 20px;
    background-color: transparent;
    border-radius:15px;
    box-shadow: 0px 0px 3px gray;
}

#burger-form label{
    font-weight: 500;
    font-size: 20px;
}

#burger-form h2{
    font-size: 55px;
    max-width: 50%;
}

h2 span{
    background-color: #42b883;
    color: white;
    width: 90%;
    display: flex;
    text-align: center;
    justify-content: center;
}

#burger-form #inputs-container{
    width: 70%;
}
#inputs-container .input-large, select{
    width: 100%;
    border-radius: 7px;
    height: 40px;
}

#all-check{
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
    align-items: center;
    justify-content: center;
}
@media screen and (max-width: 1000px){
    #burger-form{
        width: 80vw;
    }
}
@media screen and (max-width: 780px) {
    #burger-form{
        width: 90vw;
    }
}

@media screen and (max-width: 780px) {
    #burger-form{
        flex-direction: column;
    }

    #burger-form h2{
        max-width: 100%;
    }

    h2 span{
        width: 100%;
    }

    #burger-form #inputs-container{
    width: 90%;
}
}
</style>