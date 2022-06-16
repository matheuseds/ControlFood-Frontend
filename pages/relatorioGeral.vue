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
              <NuxtLink to="/dashboardSite" class="nav-link"
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
              <NuxtLink to="/relatorioGeral" class="nav-link menu-active"
                >Relatório Geral</NuxtLink
              > <button class="botaosair" @click="logout()">Sair</button>
            </b-nav>
          </nav>
          <!--end content-->
        </div>
      </div>
      <!--end menu-->
      <!--content-->
      <div class="container-content">
       
        <div class="container input-group" style="width:90%; margin-bottom:10px;">
           <input
          type="search"
          id="form1"
          class="form-control"
          v-model="pesquisa"
          placeholder="Pesquisar Empresa"
        />

          <button
            onclick="window.location.reload()"
            type="button"
            class="btn btn-dark ml-2"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="16"
              height="16"
              fill="currentColor"
              class="bi bi-search"
              viewBox="0 0 16 16"
            >
              <path
                fill-rule="evenodd"
                d="M8 3a5 5 0 1 0 4.546 2.914.5.5 0 0 1 .908-.417A6 6 0 1 1 8 2v1z"
              />
              <path
                d="M8 4.466V.534a.25.25 0 0 1 .41-.192l2.36 1.966c.12.1.12.284 0 .384L8.41 4.658A.25.25 0 0 1 8 4.466z"
              />
            </svg>
          </button>

          <button
            @click="exportPdf"
            type="submit"
            required="required"
            class="btn btn-dark imprimir"
          >
            Imprimir
          </button>
        </div>

        <div class="container">
          <table class="content-table table">
            <thead class="table-dark">
              <tr>
                <th>Nome</th>
                <th>Nome Empresa</th>
                <th>Total de Refeições</th>
                <th>Data última refeição</th>
                <th></th>
              </tr>
            </thead>

            <tbody
              v-for="colaborador in colaboradoresFiltrados"
              :key="colaborador.id"
            >
              <tr>
                <td>{{ colaborador.nome }}</td>
                <td>{{ colaborador.nome_empresa }}</td>
                <td>{{ colaborador.qtdref }}</td>
                <td>{{ new Date (colaborador.updatedAt).toLocaleString() }}</td>
              </tr>
            </tbody>
          </table>
        </div>
       
      </div>
      <!--end content-->
    </div>
  </main>
</template>

<script>
import jsPDF from 'jspdf'
import 'jspdf-autotable'

export default {
  data: () => ({
    variant: 'dark',
    variants: [
      'transparent',
      'white',
      'light',
      'dark',
      'primary',
      'secondary',
      'success',
      'danger',
      'warning',
      'info',
    ],
    colaboradores: [],

    pesquisa: '',
  }),

  async fetch() {
    this.colaboradores = await this.$axios.$get('/colaborador')
    console.log(this.colaboradores)
  },

  computed: {
    colaboradoresFiltrados() {
      return this.colaboradores.filter((colaborador) =>
        colaborador.nome_empresa
          .toLowerCase()
          .includes(this.pesquisa.toLowerCase())
      )
    },
  },
  methods: {
    exportPdf() {
      console.log(this.colaboradoresFiltrados)
      const vm = this
      const columns = [
        { title: 'Id', dataKey: 'id' },
        { title: 'Nome', dataKey: 'nome' },
        { title: 'Empresa', dataKey: 'nome_empresa' },
        { title: 'Data Última Refeição', dataKey: 'updatedAt' },
        { title: 'Total de Refeições', dataKey: 'qtdref' },
      ]
      const doc = jsPDF('p', 'pt')
      doc.text('Relatório Geral', 30, 20)
      doc.autoTable(columns, vm.colaboradoresFiltrados, {
        theme: 'striped',
      })
      doc.save('Relatório Geral .pdf')
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
/*menu*/
.nav-link {
  color: #e42021;
  transition: 0.2s;
}
.nav-link:hover {
  color: #e42021;
  transition: 0.2s;
  background: #e42021;
  color: white;
}
/*end menu*/
.btn-dark {
  background-color: #e42021;
  border:none;
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
  background-color: #e42021;
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

.botaosair {
  color: #e42021;
  border: none; 
  background-color: white;
  padding: 5% 10%;
    font-family: "WorkSansRegular";
    font-size: 18px;
    text-align: left;
}
.botaosair:hover{
  background-color: #fc8585;
  color:white;
}

.imprimir {
  margin-left: 1%;
}

.table-dark{
  font-size: "WorkSansMedium";
}
</style>
