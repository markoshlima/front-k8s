<template>
  
  <div class="container">

    <div class="container">
      <div class="row">
        <div class="col-sm">
          <h3>Busca Cliente: </h3>
        </div>
        <div class="col-sm">
          <input class="form-control" v-model="inputID">
        </div>
        <div class="col-sm">
          <button class="btn btn-primary mb-2" v-on:click="buscaCliente">Buscar</button>
        </div>
      </div>
    </div>

    <section v-if="errored">
      <p>Não encontrado ...</p>
    </section>

    <section v-else>
      <div v-if="loading">Carregando...</div>

      <div v-else>
        <div class="card card border-info mb-3">
          <div class="card-header">Dados Pessoais</div>
          <div class="card-body text-info">
            <p class="card-text">
              <b>ID:</b> {{cliente.clienteId}} <br />
              <b>Nome:</b> {{cliente.nome}} {{cliente.sobrenome}} <br />
              <b>Idade:</b> {{cliente.idade}} <br />
              <b>Documento:</b> {{cliente.documento}} <br />
            </p>
          </div>
        </div>
        <hr />

        <div class="card">
          <div class="card-header">
            Endereços
          </div>
          <div class="card-body">
            <table class="table">
              <thead>
                <tr>
                  <th scope="col">#</th>
                  <th scope="col">Rua</th>
                  <th scope="col">Numero</th>
                  <th scope="col">Bairro</th>
                  <th scope="col">Cidade</th>
                  <th scope="col">Estado</th>
                  <th scope="col">Pais</th>
                </tr>
              </thead>
              <tbody v-for="endereco of cliente.enderecos" :key="endereco">
                <tr>
                  <th scope="row">{{endereco.enderecoId}}</th>
                  <td>{{endereco.rua}}</td>
                  <td>{{endereco.numero}}</td>
                  <td>{{endereco.bairro}}</td>
                  <td>{{endereco.cidade}} </td>
                  <td>{{endereco.estado}}</td>
                  <td>{{endereco.pais}}</td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
        <hr />


        <div class="card">
          <div class="card-header">
            Compras
          </div>
          <div class="card-body">
            <div v-for="compra of cliente.compras" :key="compra">
              <div class="card border-dark mb-3">
                <div class="card-header">Número da Compra: {{compra.compraID}}</div>
                <div class="card-body text-dark">
                  <h5 class="card-title">Endereço da entrega: {{compra.endereco.rua}}, {{compra.endereco.numero}}, {{compra.endereco.bairro}}, {{compra.endereco.cidade}}/{{compra.endereco.estado}}/{{compra.endereco.pais}} <br /></h5>
                  Produtos: <br />
                  <table class="table">
                    <thead>
                      <tr>
                        <th scope="col">#</th>
                        <th scope="col">Nome</th>
                        <th scope="col">Marca</th>
                        <th scope="col">Valor</th>
                      </tr>
                    </thead>
                    <tbody v-for="produto of compra.produtos" :key="produto">
                      <tr>
                        <th scope="row">{{produto.produtoID}} </th>
                        <td>{{produto.nome}} </td>
                        <td>{{produto.marca}} </td>
                        <td>{{produto.valor}} </td>
                      </tr>
                    </tbody>
                  </table>
                </div>
                <div class="card text-white bg-success mb-3" style="margin: 15px">
                  <div class="card-header">Pagamento</div>
                  <div class="card-body">
                    <div class="card-text">
                      <b>Valor Total de Produtos:</b> {{compra.valor}} <br />
                      <div v-if="compra.descontoNome">
                        <b>Desconto:</b> {{compra.descontos}} ({{compra.descontoNome}})<br />
                      </div>
                      <b>Total da Compra:</b> {{compra.total}} <br />
                      <b>Método de Pagamento:</b> {{compra.pagamento}} <br />
                      <b>Data:</b> {{compra.data}} <br />
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

    </section>
    
  </div> 

</template>
<script>
  import axios from 'axios';

  export default {
    name: 'ClienteComponent',
    data() {
      return {
        cliente: null,
        loading: true,
        errored: false,
        inputID: "1"
      };
    },
    created: function() {
    },
    methods: {
      buscaCliente: function(){
        axios
          .get('http://localhost:5005/cliente-geral/'+this.inputID)
          .then(res => {
            this.errored = false
            this.cliente = res.data;
            console.log(this.cliente);
          })
          .catch(error => {
            console.log(error)
            this.errored = true
        })
        .finally(() => this.loading = false)
      }
    }
  }
</script>
<style>
  h3 {
    margin-bottom: 5%;
  }
</style>