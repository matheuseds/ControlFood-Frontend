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
            <NuxtLink to="/listarEmpresas" class="nav-link"
              >Listar Empresas</NuxtLink
            >
          </li>
          <li class="nav-item active">
            <NuxtLink to="/relatorioGeral" class="nav-link"
              >Relatorios</NuxtLink
            >
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
          placeholder="Pesquisar Colaborador"
        />
      </div>
      <button type="button" class="btn btn-dark">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="16"
          height="16"
          fill="currentColor"
          class="bi bi-search"
          viewBox="0 0 16 16"
        >
          <path
            d="M11.742 10.344a6.5 6.5 0 1 0-1.397 1.398h-.001c.03.04.062.078.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1.007 1.007 0 0 0-.115-.1zM12 6.5a5.5 5.5 0 1 1-11 0 5.5 5.5 0 0 1 11 0z"
          />
        </svg>
      </button>
    </div>

    <h1 class="titulo">Colaboradores Cadastrados</h1>
    <div class="container">
      <table class="table">
        <thead class="table-dark">
          <tr>
            <th>Id</th>
            <th>Nome</th>
            <th>CPF</th>
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
            <td>{{ colaborador.cpf }}</td>
            <td>{{ colaborador.nome_empresa }}</td>
            <td>{{ colaborador.email }}</td>
            <td>
              <b-button
                style="background-color: #b33939"
                v-b-modal.modal-excluir
                @click="id = colaborador.id"
              >
                <b-icon-trash></b-icon-trash>
              </b-button>

              <b-button
                style="background-color: #2980b9"
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
      this.$fetch()
    },
    abrirModaldeEdicao(colaborador) {
      this.colaborador = Object.assign({}, colaborador)
    },

    async excluirColaborador() {
      await this.$axios.$delete(`/colaborador/${this.id}`)
      const filterColaboradores = this.colaboradores.filter((colaborador) => 
      colaborador.id !== this.id
    
      )

      this.colaboradores = filterColaboradores
    },
  },
}
</script>
<style>
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
.form-control {
  margin-bottom: 3%;
}
.row {
  justify-content: center;
}
</style>
