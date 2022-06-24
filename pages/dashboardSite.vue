<template>
  <main class="background">
    <div class="container-naosei">
      <!--menu-->
      <div class="menu-bar">
        <div class="py-2">
          <!--content-->
          <nav class="mb-3">
            <b-nav vertical>
              <div style="text-align: center; margin: 4% 0px 17%">
                <b-img
                  class="img-menu"
                  src="https://designerelite.com.br/images/logo.png"
                  fluid
                  alt="Responsive image"
                ></b-img>
              </div>
              <NuxtLink to="/dashboardSite" class="nav-link menu-active"
                >Dashboard</NuxtLink
              >
              <NuxtLink to="/cadastrarEmpresa" class="nav-link"
                >Cadastrar Empresa</NuxtLink
              >
              <NuxtLink to="/cadastrarColaborador" class="nav-link"
                >Cadastrar Colaborador</NuxtLink
              >
              <NuxtLink to="/listarColaboradores" class="nav-link"
                >Listar Colaboradores</NuxtLink
              >
              <NuxtLink to="/listarEmpresas" class="nav-link"
                >Listar Empresas</NuxtLink
              >
              <NuxtLink to="/relatorioGeral" class="nav-link"
                >Relatório Geral</NuxtLink
              >
              <button class="botaosair" @click="logout()">Sair</button>
            </b-nav>
          </nav>
          <!--end content-->
        </div>
      </div>
      <!--end menu-->
      <div class="container-content">
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
          <div class="container">
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

          <!-- ARRUMAR TITULO <h1 class="titulo">Colaboradores</h1> -->
          <div class="container">
            <table class="content-table table">
              <thead class="table-title">
                <h1>Colaboradores</h1>
              </thead>
              <div>
                <b-modal
                  id="modal-check"
                  title="Confirmar refeição"
                  ok-title="Sim"
                  cancel-title="Não"
                  @ok="confirmarRefeicao(id)"
                >
                  <p class="my-4">Confirmar refeição do colaborador ?</p>
                </b-modal>
              </div>

              <tbody
                v-for="colaborador in colaboradoresFiltrados"
                :key="colaborador.id"
              >
                <div class="table-row">
                  <div class="table-id">
                    <h1>{{ colaborador.id }}</h1>
                  </div>
                  <div class="table-user">
                      <h1>{{ colaborador.nome }}</h1>
                      <div class="table-user-description">
                      <p>{{ colaborador.nome_empresa }}</p>
                    </div>
                  </div>
                  <div class="table-btn">
                    <b-button
                      v-b-modal.modal-check
                      @click="id = colaborador.id"
                    >
                      <b-icon-check style="font-size: 30px !important;"></b-icon-check>
                    </b-button>
                  </div>
                </div>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  data: () => ({
    colaborador: {
      id: '',
    },

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
  beforeCreate() {
    // função  para voltar para o login caso não esteja logado
    const localToken = localStorage.getItem('token')
    if (!localToken) {
      this.$router.push({ name: 'index' })
    }
  },
  methods: {
    logout() {
      localStorage.removeItem('token')
      localStorage.removeItem('id')
      this.$router.push({ name: 'index' })
    },

    async confirmarRefeicao(id) {
      try {
        await this.$axios.$post('/colaborador/addref', { id })
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

@font-face {
  font-family: "WorkSansRegular";
  src: url("fontes/WorkSans-Regular.ttf");
}
@font-face {
  font-family: "WorkSansMedium";
  src: url("fontes/WorkSans-Medium.ttf");
}
@font-face {
  font-family: "WorkSansSemiBold";
  src: url("fontes/WorkSans-SemiBold.ttf");
}
@font-face {
  font-family: "WorkSansBold";
  src: url("fontes/WorkSans-Bold.ttf");
}

* {
  font-family: sans-serif;
}

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

.card-title {
  font-size:  "WorkSansMedium";
  font-weight: bolder;
}

.icons {
  margin-left: 38%;
}
.pesquisa {
  width: 90%;
  margin: 0 auto;
}
</style>
