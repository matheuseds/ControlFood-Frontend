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
    <div class="row">
      <div class="card" style="width: 17rem">
        <div class="card-body">
          <h5 class="card-title">Empresas Cadastradas</h5>
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="60"
            height="40"
            fill="currentColor"
            class="bi bi-briefcase-fill icons"
            viewBox="0 0 16 16"
          >
            <path
              d="M6.5 1A1.5 1.5 0 0 0 5 2.5V3H1.5A1.5 1.5 0 0 0 0 4.5v1.384l7.614 2.03a1.5 1.5 0 0 0 .772 0L16 5.884V4.5A1.5 1.5 0 0 0 14.5 3H11v-.5A1.5 1.5 0 0 0 9.5 1h-3zm0 1h3a.5.5 0 0 1 .5.5V3H6v-.5a.5.5 0 0 1 .5-.5z"
            />
            <path
              d="M0 12.5A1.5 1.5 0 0 0 1.5 14h13a1.5 1.5 0 0 0 1.5-1.5V6.85L8.129 8.947a.5.5 0 0 1-.258 0L0 6.85v5.65z"
            />
          </svg>
          <p class="card-text">{{ empresas.length }}</p>
        </div>
      </div>
      <div class="card" style="width: 17rem">
        <div class="card-body">
          <h5 class="card-title">Total de Colaboradores</h5>
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="60"
            height="40"
            fill="currentColor"
            class="bi bi-person-check-fill icons"
            viewBox="0 0 16 16"
          >
            <path
              fill-rule="evenodd"
              d="M15.854 5.146a.5.5 0 0 1 0 .708l-3 3a.5.5 0 0 1-.708 0l-1.5-1.5a.5.5 0 0 1 .708-.708L12.5 7.793l2.646-2.647a.5.5 0 0 1 .708 0z"
            />
            <path
              d="M1 14s-1 0-1-1 1-4 6-4 6 3 6 4-1 1-1 1H1zm5-6a3 3 0 1 0 0-6 3 3 0 0 0 0 6z"
            />
          </svg>
          <p class="card-text">{{ colaboradores.length }}</p>
        </div>
      </div>
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

      <!-- ARRUMAR TITULO <h1 class="titulo">Colaboradores</h1> -->
      <div class="container">
        <table class="table">
          <thead class="table-dark">
            <tr>
              <th>Id</th>
              <th>Nome</th>
              <th>CPF</th>
              <th>Nome Empresa</th>
              <th></th>
            </tr>
          </thead>

          <div>
            <b-modal
              id="modal-check"
              title="Confirmar refeição"
              ok-title="Sim"
              cancel-title="Não"
              @ok="confirmarRefeicao()"
            >
              <p class="my-4">Confirmar refeição do colaboardor ?</p>
            </b-modal>
          </div>

          <tbody
            v-for="colaborador in colaboradoresFiltrados"
            :key="colaborador.id"
          >
            <tr>
              <td>{{ colaborador.id }}</td>
              <td>{{ colaborador.nome }}</td>
              <td class="alinhar">{{ colaborador.cpf }}</td>
              <td>{{ colaborador.nome_empresa }}</td>
              <td>
                <b-button style="background-color: #16a085"
                 v-b-modal.modal-check
                @click="id = colaborador.id"
                >
                  <b-icon-check></b-icon-check>
                </b-button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  data: () => ({
    empresas: [],
    colaboradores: [],
    pesquisa: '',
  }),
  async fetch() {
    this.empresas = await this.$axios.$get('/empresa')
    this.colaboradores = await this.$axios.$get('/colaborador')
  },
  computed: {
    colaboradoresFiltrados() {
      return this.colaboradores.filter((colaborador) =>
        colaborador.nome.toLowerCase().includes(this.pesquisa.toLowerCase())
      )
    },
  },
}
</script>

<style>
.card {
  display: inline-block;
  margin-top: 1% !important;
  margin-left: 5%;
  margin-right: 5%;
  box-shadow: 1px 3px 3px rgba(0, 0, 0, 0.459);
}

.row {
  justify-content: center;
}
.card-text {
  text-align: center;
  font-weight: bold;
}

.icons {
  margin-left: 38%;
}
</style>
