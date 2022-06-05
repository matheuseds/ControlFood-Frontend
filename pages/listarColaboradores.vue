<template>
  <main class="background">
    <nav class="navbar navbar-expand navbar-dark " style="background-color: #009879;">
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
            <NuxtLink to="/listarEmpresas" class="nav-link"
              >Listar Empresas</NuxtLink
            >
          </li>
          <li class="nav-item active">
            <NuxtLink to="/relatorioGeral" class="nav-link"
              >Relatórios</NuxtLink
            >
          </li>
          <li>
            <button class="botaosair" @click="logout()">Sair</button>
          </li>
        </ul>
      </div>
    </nav>

    <div class="container input-group pesquisa1">
      <div class="pesquisa">
        <input
          type="search"
          id="form1"
          class="form-control"
          v-model="pesquisa"
          placeholder="Pesquisar Colaborador"
        />
      </div>
    </div>

    <h1 class="titulo">Colaboradores Cadastrados</h1>
    <div class="container">
      <b-alert :variant="responseColor" :show="showAlert">{{
        responseMessage
      }}</b-alert>


      <table class="content-table table" >
        <thead class="table-dark" >
          <tr>
            <th>Id</th>
            <th>Nome</th>
            <th>Empresa</th>
            <th>E-mail</th>
            <th></th>
          </tr>
        </thead>
        <div>
          <b-modal
            id="modal-excluir"
            title="Excluir colaborador"
            ok-title="Sim"
            cancel-title="Não"
            @ok="excluirColaborador()"
          >
            <p class="my-4">Você deseja excluir este colaborador(a)?</p>
          </b-modal>
        </div>

        <b-modal
          id="modal-editar"
          title="Editar Colaborador"
          ok-title="Confirmar"
          cancel-title="Cancelar"
          @ok="editarColaborador()"
        >
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
        </b-modal>
        <tbody
          v-for="colaborador in colaboradoresFiltrados"
          :key="colaborador.id"
        >
          <tr>
            <td>{{ colaborador.id }}</td>
            <td>{{ colaborador.nome }}</td>
            <td>{{ colaborador.nome_empresa }}</td>
            <td>{{ colaborador.email }}</td>
            <td>
              <b-button
                style="background-color: #CF1506"
                v-b-modal.modal-excluir
                @click="id = colaborador.id"
              >
                <b-icon-trash></b-icon-trash>
              </b-button>

              <b-button
                style="background-color: #007BFF"
                v-b-modal.modal-editar
                @click="abrirModaldeEdicao(colaborador)"
              >
                <b-icon-pencil></b-icon-pencil>
              </b-button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </main>
</template>

<script>
export default {
  data: () => ({
    colaborador: {
      nome: '',
      cpf: '',
      nome_empresa: '',
      email: '',
      id: '',
    },
    colaboradores: [],
    pesquisa: '',

    responseColor: null,
    responseMessage: null,
    showAlert: false,
  }),

  async fetch() {
    this.colaboradores = await this.$axios.$get('/colaborador')
  },

  computed: {
    colaboradoresFiltrados() {
      return this.colaboradores.filter((colaborador) =>
        colaborador.nome.toLowerCase().includes(this.pesquisa.toLowerCase())
      )
    },
  },

  methods: {

  

    async editarColaborador() {
      await this.$axios.$put(
        `/colaborador/${this.colaborador.id}`,
        this.colaborador
      )

      try {
        const response = await this.$axios.$put(
          `/colaborador/${this.colaborador.id}`
        )
        this.responseColor = 'success'
        this.responseMessage = response.message
        this.showAlert = true
      } catch (error) {
        this.responseColor = 'danger'
        this.responseMessage = 'Ocorreu um erro'
        this.showAlert = true
      }

      this.$fetch()
    },

    abrirModaldeEdicao(colaborador) {
      this.colaborador = Object.assign({}, colaborador)
    },

    async excluirColaborador() {
      await this.$axios.$delete(`/colaborador/${this.id}`)

      try {
        const response = await this.$axios.$delete(`/colaborador/${this.id}`)
        this.responseColor = 'success'
        this.responseMessage = response.message
        this.showAlert = true
      } catch (error) {
        this.responseColor = 'danger'
        this.responseMessage = 'Ocorreu um erro'
        this.showAlert = true
      }

      const filterColaboradores = this.colaboradores.filter(
        (colaborador) => colaborador.id !== this.id
      )

      this.colaboradores = filterColaboradores
    },
     logout() {
      localStorage.removeItem('token')
      localStorage.removeItem('id')
      this.$router.push({ name: 'index' })
    },
  },
}
</script>

<style>

* {
  font-family: sans-serif; 
}

.titulo {
  margin-top: 2%;
  text-align: center;
  margin-bottom: 3%;
}
.pesquisa {
  align-items: center;
  margin-left: 20%;
  margin-top: 2%;
  width: 60%;
}

.input-group {
    position: relative;
    /* display: flex; */
    flex-wrap: wrap;
    align-items: stretch;
    width: 100%;
}

.pesquisa1 {
  align-items: center;
  margin-left: 20%;
  margin-top: 2%;
  width: 60%;
 
}

.form-control {
  margin-bottom: 3%;
}
.row {
  justify-content: center;
}

.content-table {
  border-collapse: collapse;
  margin: 25px 0;
  font-size: 0.9em;
  min-width: 400px;
  border-radius: 5px 5px 0 0;
  overflow: hidden;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.15);
}

.content-table thead tr {
  background-color: #009879;
  color: #ffffff;
  font-weight: bold;
}

.content-table th,
.content-table td {
  padding: 12px 15px;
}

.content-table tbody tr {
  border-bottom: 1px solid #dddddd;
}

.content-table tbody tr:nth-of-type(even) {
  background-color: #f3f3f3;
}

.content-table tbody tr:last-of-type {
  border-bottom: 2px solid #009879;
}

.botaosair{
  background-color: #009879;
  color: #fff;
  border:none;
  padding:27%;
}


</style>
