<template>
  <main class="background">
    <nav
      class="navbar navbar-expand navbar-dark"
      style="background-color: #009879"
    >
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

    <div class="container input-group pesquisa">
      <div class="pesquisa">
        <input
          type="search"
          id="form1"
          class="form-control"
          v-model="pesquisa"
          placeholder="Pesquisar Empresas"
        />
      </div>
    </div>

    <h1 class="titulo">Empresas Cadastradas</h1>
    <div class="container">
      <b-alert :variant="responseColor" :show="showAlert">{{
        responseMessage
      }}</b-alert>

      <table class="content-table table">
        <thead class="table-dark">
          <tr>
            <th>Id</th>
            <th>Empresa</th>
            <th>Contato do Responsável</th>
            <th>E-mail</th>
            <th></th>
          </tr>
        </thead>

        <div>
          <b-modal
            id="modal-1"
            title="Excluir empresa"
            ok-title="Sim"
            cancel-title="Não"
            @ok="excluirEmpresa()"
          >
            <p class="my-4">Você deseja excluir esta empresa?</p>
          </b-modal>
        </div>

        <b-modal
          id="modal-editarempresa"
          title="Editar Empresa"
          ok-title="Confirmar"
          cancel-title="Cancelar"
          @ok="editarEmpresa()"
        >
          <div class="form-group">
            <label for="number">Nome da empresa:</label>
            <input
              v-model="empresa.nomeEmpresa"
              class="form-control"
              type="text"
              placeholder="Nome da Empresa"
              required
            />
          </div>

          <div class="form-group">
            <label for="email">E-mail:</label>
            <input
              v-model="empresa.email"
              class="form-control"
              type="email"
              placeholder="E-mail"
              required
            />

            <div class="form-group">
              <label for="email">Nome do responsável:</label>
              <input
                v-model="empresa.nomeResponsavel"
                class="form-control"
                type="text"
                placeholder="Nome da Empresa"
                required
              />
            </div>

            <div class="form-group">
              <label for="email">Contato do responsável:</label>
              <input
                v-model="empresa.contatoResponsavel"
                class="form-control"
                type="text"
                placeholder="Contato do Responsável"
                required
              />
            </div>

            <div class="form-group">
              <label for="email">Endereço:</label>
              <input
                v-model="empresa.endereco"
                class="form-control"
                type="text"
                placeholder="Endereço da Empresa"
                required
              />
            </div>

            <div class="form-group">
              <label for="email">Cidade:</label>
              <input
                v-model="empresa.cidade"
                class="form-control"
                type="text"
                placeholder="Cidade"
                required
              />
            </div>

            <div class="form-group">
              <label for="email">Estado:</label>
              <input
                v-model="empresa.estado"
                class="form-control"
                type="text"
                placeholder="Estado"
                required
              />
            </div>
          </div>
        </b-modal>

        <tbody v-for="empresa in empresasFiltradas" :key="empresa.id">
          <tr>
            <td>{{ empresa.id }}</td>
            <td>{{ empresa.nomeEmpresa }}</td>
            <td>{{ empresa.contatoResponsavel }}</td>
            <td>{{ empresa.email }}</td>
            <td>
              <b-button
                style="background-color: #cf1506"
                v-b-modal.modal-1
                @click="id = empresa.id"
              >
                <b-icon-trash></b-icon-trash>
              </b-button>

              <b-button
                style="background-color: #007bff"
                v-b-modal.modal-editarempresa
                @click="abrirModaldeEdicao(empresa)"
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
    empresa: {
      nomeEmpresa: '',
      nomeResponsavel: '',
      email: '',
      contatoResponsavel: '',
      endereco: '',
      cidade: '',
      estado: '',
      id: '',
    },

    empresas: [],
    pesquisa: '',
    id: null,

    responseColor: null,
    responseMessage: null,
    showAlert: false,
  }),
  async fetch() {
    this.empresas = await this.$axios.$get('/empresa')
  },
  computed: {
    empresasFiltradas() {
      return this.empresas.filter((empresa) =>
        empresa.nomeEmpresa.toLowerCase().includes(this.pesquisa.toLowerCase())
      )
    },
  },
  methods: {
    async excluirEmpresa() {
      await this.$axios.$delete(`/empresa/${this.id}`)

      try {
        const response = await this.$axios.$delete(`/empresa/${this.id}`)
        this.responseColor = 'success'
        this.responseMessage = response.message
        this.showAlert = true
      } catch (error) {
        this.responseColor = 'danger'
        this.responseMessage = 'Ocorreu um erro'
        this.showAlert = true
      }

      const filterEmpresas = this.empresas.filter(
        (empresa) => empresa.id !== this.id
      )

      this.empresas = filterEmpresas
    },

    async editarEmpresa() {
      await this.$axios.$put(`/empresa/${this.empresa.id}`, this.empresa)

      try {
        const response = await this.$axios.$put(`/empresa/${this.empresa.id}`)
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

    abrirModaldeEdicao(empresa) {
      this.empresa = Object.assign({}, empresa)
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

.input-group {
  position: relative;
  /* display: flex; */
  flex-wrap: wrap;
  align-items: stretch;
  width: 100%;
}

.pesquisa {
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

.botaosair {
  background-color: #009879;
  color: #fff;
  border: none;
  padding: 27%;
}
</style>
