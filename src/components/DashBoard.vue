<template>
    <div id="dashboard">
        <table>
            <thead>
                <tr>
                    <th>#</th>
                    <th>Cliente</th>
                    <th>Carne</th>
                    <th>Pão</th>
                    <th>Opcionais</th>
                    <th>Ações</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="burger in burgers" :key="burger.id" >
                    <td>{{ burger.id }}</td>
                    <td>{{ burger.nome }}</td>
                    <td>{{burger.carne}}</td>
                    <td>{{ burger.pao }}</td>
                    <td>
                        <ul>
                            <li v-for="(opcional, index) in burger.opcionais" :key="index">{{opcional}}</li>

                        </ul>
                    </td>
                    <td id="acoes">
                            <select name="status" id="status" @change="ChangeStatus($event, burger.id)">
                                <option value="" selected>Selecione</option>
                                <option v-for="s in status" :key="s.id" :value="s.tipo" :selected="burger.status == s.tipo">{{s.tipo}}</option>  
                            </select>
                            <button class="btn btn-danger" @click="RemovePedido(burger.id)">Cancelar</button>
                    </td>
                </tr>

            </tbody>
        </table>

        <MyMessage :msg="message" v-show="message"/>
    </div>
</template>

<script>
import MyMessage from '../components/MyMessage';

export default {
    name: "DashBoard",
    components:{MyMessage},
    data(){
        return {
            burgers: null,
            burgers_id: null,
            status: [],
            message: ""
        };
    },
    methods:{
        async getBurgers(){
            const request = await fetch("http://localhost:3000/burgers")
            const data = await request.json()
            this.burgers = data
        },
        async getStatus(){
            const request = await fetch("http://localhost:3000/status")
            const data = await request.json()
            this.status = data

        },
        async RemovePedido(id){
            const request = await fetch(`http://localhost:3000/burgers/${id}`,{
                method: "DELETE",
                headers: {"Content-Type": "application/json"}
            })
            const data = await request.json()
            this.getBurgers()

            this.message = `Pedido N° #${data.id} foi excluído com sucesso!`

            setTimeout(()=> this.message = "", 4000)
        },
        async ChangeStatus(event, id){

            const option = event.target.value
            //const ObjJson = JSON.stringify({status: option})

            const request = await fetch(`http://localhost:3000/burgers/${id}`, {
                method: "PATCH",
                headers: {"Content-Type": "application/json"},
                body: JSON.stringify({status: option})
            })

            const data = await request.json()

            this.message = `Pedido N° #${data.id} foi modificado para ${data.status}!`

            setTimeout(()=> this.message = "", 4000)
        }
    },
    mounted(){
        this.getBurgers()
        this.getStatus()
    }
}
</script>

<style scoped>

    #msg-content{
        position: absolute;
        bottom: 78vh;
        left: 60vw;
        min-width: 37vw;
    }
    #dashboard{
        width: 100%;
        overflow-x: auto;

    }
    #dashboard table{
        min-width: 100%;
        border-radius: 20px;
    }

    #dashboard td, th{
        text-align: center;
        width: 300px;
        padding: 5px;
    }

    #dashboard thead{
        background-color: white;
        border-bottom: 1px solid #1a1a1a;
    }

    #acoes{
        display: flex;
        padding: 10% 0px !important;
        justify-content: space-between;
    }

    #acoes select, button{
        width: 45%;
    }

    #acoes select{
        border-radius: 5px;
    }

    tbody tr{
        border-bottom: 1px solid #1a1a1a;
    }

    @media screen and (max-width: 780px){
        #acoes{
            flex-direction: column;
            align-items: center;
            gap: 20px;
            padding: 25% 0px;
            justify-content: space-around;
        }
        #acoes select, button{
            width: 100%;
        }
        #dashboard td, th{
            text-align: center;
            width: auto;
            padding: 5px;
        }
        #acoes select{
            order: 1;
        }
        #acoes button{
            order: 0;
        }
    }

    @media screen and (max-width: 500px){
    }

</style>