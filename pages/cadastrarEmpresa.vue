<template>
  <main>
   <nav class="navbar navbar-expand navbar-dark bg-dark">
     <NuxtLink to="/dashboardSite" class="navbar-brand" >Control Food</NuxtLink>

      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarsExample02"
        aria-controls="navbarsExample02"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarsExample02">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item active">
            <NuxtLink to="/cadastrarEmpresa" class="nav-link" >Cadastrar Empresas</NuxtLink>
          </li>
          <li class="nav-item active">
            <NuxtLink to="/cadastrarColaborador" class="nav-link" >Cadastrar Colaborador</NuxtLink>
          </li>
          <li class="nav-item active">
            <NuxtLink to="/listarColaboradores" class="nav-link" >Listar Colaboradores</NuxtLink>
          </li>
          <li class="nav-item active">
            <NuxtLink to="/relatorioGeral" class="nav-link" >Relatorios</NuxtLink>
          </li>
        </ul>
      </div>
    </nav>
    <div class="container">
      <div class="row">
        <div class="col-6">
          <div class="card">
            <div class="card-body">
              <h1>Cadastrar Empresa</h1>
              <form id="form-contato">
                <div class="form-group">
                  <label for="nome">CNPJ:</label>
                  <input
                    class="form-control"
                    type="text"
                    name="nome"
                    id="cnpj"
                    placeholder="CNPJ"
                    v-maska="'##.###.###/####-##'"
                    required
                  />
                </div>
                <div class="form-group">
                  <label for="email">Nome da empresa:</label>
                  <input
                    class="form-control"
                    type="text"
                    name="nome"
                    id="nomeEmpresa"
                    placeholder="Nome da Empresa"
                    required
                  />
                </div>
                <div class="form-group">
                  <label for="email">E-mail:</label>
                  <input
                    class="form-control"
                    type="email"
                    name="email"
                    id="emailEmpresa"
                    placeholder="E-mail"
                    required
                  />
                </div>
                <div class="form-group">
                  <label for="email">Nome do Responsável:</label>
                  <input
                    class="form-control"
                    type="text"
                    name="nome"
                    id="nomeResponsavel"
                    placeholder="Nome da Empresa"
                    required
                  />
                </div>
                <div class="form-group">
                  <label for="email">Contato do Responsável:</label>
                  <input
                    class="form-control"
                    type="text"
                    name="nome"
                    id="contatoEmpresa"
                    placeholder="Contato do Responsável"
                    required
                  />
                </div>
                <div class="form-group">
                  <label for="inputAddress">Endereço</label>
                  <input
                    type="text"
                    class="form-control"
                    id="endereco"
                    placeholder="Rua Major Gote, n° 808"
                    required
                  />
                </div>
                <div class="form-row">
                  <div class="form-group col-md-6">
                    <label for="inputCity">Cidade</label>
                    <input
                      type="text"
                      class="form-control"
                      id="cidade"
                      placeholder="Patos de Minas"
                      required
                    />
                  </div>
                  <div class="form-group col-md-3">
                    <label for="inputEstado">Estado</label>
                    <input
                      type="text"
                      class="form-control"
                      id="estado"
                      placeholder="MG"
                      v-maska="'##'"
                      required
                    />
                  </div>
                  <div class="form-group col-md-4">
                    <label for="inputCEP">CEP</label>
                    <input type="number" 
                    class="form-control" 
                    id="cep" 
                    placeholder="38702-054"
                    v-maska="'#####-###'"
                    required />
                  </div>
                </div>

                <div class="form-group text-center">
                  <button type="submit" class="btn btn-dark">ENVIAR</button>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>

import { maska } from 'maska'

export default {
    directives: { maska },

    data: () => ({
     cadastrarEmpresa:{ 
      nome:'',
      cpf:'',
      nomeEmpresa:'',
      email:'',
      numeroMatricula:''

    }
  }),

  methods: {
    login() {
      alert('login')
    },
  },
}
</script>

<style>
.row {
  justify-content: center;
}
</style>