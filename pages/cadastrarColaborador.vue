<template>
  <main class="background">
    <nav class="navbar navbar-expand navbar-dark bg-dark">
      <NuxtLink to="/dashboardSite" class="navbar-brand">Control Food</NuxtLink>

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
            <NuxtLink to="/cadastrarEmpresa" class="nav-link"
              >Cadastrar Empresas</NuxtLink
            >
          </li>
          <li class="nav-item active">
            <NuxtLink to="/cadastrarColaborador" class="nav-link"
              >Cadastrar Colaborador</NuxtLink
            >
          </li>
          <li class="nav-item active">
            <NuxtLink to="/listarColaboradores" class="nav-link"
              >Listar Colaboradores</NuxtLink
            >
          </li>
           <li class="nav-item active">
            <NuxtLink to="/listarEmpresas" class="nav-link" >Listar Empresas</NuxtLink>
          </li>
          <li class="nav-item active">
            <NuxtLink to="/relatorioGeral" class="nav-link"
              >Relatorios</NuxtLink
            >
          </li>
        </ul>
      </div>
    </nav>
    <div class="container">
      <div class="row">
        <div class="col-6">
          <div class="card">
            <div class="card-body">
              <h1>Cadastrar Colaboradores</h1>
              <form @submit.prevent="cadastro">
                <b-alert :variant="responseColor" :show="showAlert">{{
                  responseMessage
                }}</b-alert>

                <div class="form-group">
                  <label for="email">Nome:</label>
                  <input
                    v-model="colaborador.nome"
                    class="form-control"
                    type="text"
                    placeholder="Nome"
                    required
                  />
                </div>
                <div class="form-group">
                  <label for="number">CPF:</label>
                  <input
                    v-model="colaborador.cpf"
                    class="form-control"
                    type="text"
                    placeholder="303.810.860-03"
                    v-maska="'###.###.###-##'"
                    required
                  />
                </div>

                <div class="form-group">
                  <label for="email">Nome da Empresa:</label>
                  <input
                    v-model="colaborador.nome_empresa"
                    class="form-control"
                    type="text"
                    placeholder="Nome da Empresa"
                    required
                  />
                </div>
                <div class="form-group">
                  <label for="email">E-mail:</label>
                  <input
                    v-model="colaborador.email"
                    class="form-control"
                    type="email"
                    placeholder="E-mail"
                    required
                  />
                </div>
                <div class="form-group">
                  <label for="email">Número de Matricula:</label>
                  <input
                    v-model="colaborador.numero_matricula"
                    class="form-control"
                    type="text"
                    placeholder="Número da Matricula"
                    required
                  />
                </div>

                <div class="container form-group text-center botao">
                  <button type="submit" class="btn btn-dark" required>
                    ENVIAR
                  </button>
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
    colaborador: {
      nome: '',
      cpf: '',
      nome_empresa: '',
      email: '',
      numero_matricula: '',
    },
    responseColor: null,
    responseMessage: null,
    showAlert: false,
  }),

  methods: {
    async cadastro() {
      /**
       * Post = Enviar dados
       * Get = Receber dados
       * Patch = Atualizar dados
       * Delete = Excluir dados
       */
      try {
        const response = await this.$axios.$post(
          '/colaborador',
          this.colaborador
        )
        this.responseColor = 'success'
        this.responseMessage = response.message
        this.showAlert = true
      } catch (error) {
        this.responseColor = 'danger'
        this.responseMessage = 'Ocorreu um erro'
        this.showAlert = true
      }
    },
  },
}
</script>

<style>



.botao {
  margin-top: 7%;
}
.row {
  margin-top: 5%;
  justify-content: center;
}
</style>
