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
          placeholder="Pesquisar Empresas"
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

    <h1 class="titulo">Empresas Cadastradas</h1>
    <div class="container">
      <table class="table">
        <thead class="table-dark">
          <tr>
            <th>Id</th>
            <th>CNPJ</th>
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
            <label for="email">CNPJ:</label>
            <input
              v-model="empresa.cnpj"
              class="form-control"
              type="number"
              placeholder="CNPJ"
              v-maska="'##.###.###/####-##'"
              required
            />
          </div>
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
            <td>{{ empresa.cnpj }}</td>
            <td>{{ empresa.nomeEmpresa }}</td>
            <td>{{ empresa.contatoResponsavel }}</td>
            <td>{{ empresa.email }}</td>
            <td>
              <b-button
                style="background-color: #b33939"
                v-b-modal.modal-1
                @click="id = empresa.id"
              >
                <b-icon-trash></b-icon-trash>
              </b-button>

              <b-button
                style="background-color: #2980b9"
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
      cnpj: '',
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
      const filterEmpresas = this.empresas.filter(
        (empresa) => empresa.id !== this.id
      )

      this.empresas = filterEmpresas
    },

    async editarEmpresa() {
      await this.$axios.$put(`/empresa/${this.empresa.id}`, this.empresa)
      this.$fetch()
    },

    abrirModaldeEdicao(empresa) {
      this.empresa = Object.assign({}, empresa)
    },
  },
}
</script>

<style>
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
