<template>
    <div>
        <h1> Cadastro de Clientes</h1>
        <form>
            <div class="mb-3">
                <label class="form-label">CNPJ</label>
                <input type="text" class="form-control" placeholder="Informe o seu CNPJ" v-model="cliente.CNPJ">
            </div>
            <div>
                <label class="form-label">Nome</label>
                <input type="text" class="form-control" placeholder="Informe o seu nome" v-model="cliente.Nome">
            </div>
            <div>
                <label class="form-label">Endereco</label>
                <input type="text" class="form-control" placeholder="Informe o seu endereço" v-model="cliente.Endereco">
            </div>
            <div>
                <label class="form-label">Contato</label>
                <input type="text" class="form-control" placeholder="Informe o seu meio de contato" v-model="cliente.Contato">
            </div>
            <button class="btn btn-primary" v-on:click="salvarCliente(cliente)">Salvar</button>
        </form>
        <div>
            <table class="table">
            <thead>
                <tr>
                    <th scope="col">#</th>
                    <th scope="col">CNPJ</th>
                    <th scope="col">Nome</th>
                    <th scope="col">Endereço</th>
                    <th scope="col">Contato</th>
                </tr>
            </thead>
            <tbody v-for="cliente of clientes" :key="cliente.id">
                 <td>{{cliente.id}}</td>
                 <td>{{cliente.cnpj}}</td>
                 <td>{{cliente.nome}}</td>
                 <td>{{cliente.endereco}}</td>
                 <td>{{cliente.contato}}</td>
            </tbody>
        </table>
        </div>
    </div>
</template>

<script>
import api from '@/services/api'
export default {
    name: "Cliente",
    data(){
        return{
            cliente:{
                CNPJ:'',
                Nome:'',
                Endereco:'',
                Contato:''
            },
            clientes: []
        }
    },
    mounted(){
        this.carregarClientes()
    },
    methods:{
        carregarClientes(){
            api.get('/api/Clientes').then(response =>{
                console.log(response.data)
                this.clientes = response.data
            })
        },
        salvarCliente(cliente){
            api.post('/api/Clientes', cliente)
        }
    }
}
</script>

<style scoped>
    .form-control{
        width: 50%;
    }
    button{
        margin-top: 30px;
    }
    table{
        margin-top: 30px;
        width: 50%;
    }
</style>