<template>
  <main class="background">
    <nav class="navbar navbar-expand navbar-dark" style="background-color: #009879;">
      <NuxtLink to="/dashboardSite" class="navbar-brand">Control Food</NuxtLink>

      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarsExample02"
        aria-controls="navbarsExample02" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarsExample02">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item active">
            <NuxtLink to="/cadastrarEmpresa" class="nav-link">Cadastrar Empresas</NuxtLink>
          </li>
          <li class="nav-item active">
            <NuxtLink to="/cadastrarColaborador" class="nav-link">Cadastrar Colaborador</NuxtLink>
          </li>
          <li class="nav-item active">
            <NuxtLink to="/listarColaboradores" class="nav-link">Listar Colaboradores</NuxtLink>
          </li>
          <li class="nav-item active">
            <NuxtLink to="/listarEmpresas" class="nav-link">Listar Empresas</NuxtLink>
          </li>
          <li class="nav-item active">
            <NuxtLink to="/relatorioGeral" class="nav-link">Relatórios</NuxtLink>
          </li>
          <li>
            <button class="botaosair" @click="logout()">Sair</button>
          </li>
        </ul>
      </div>
    </nav>

    <div class="container input-group pesquisa">
      <div class="pesquisa">
        <input type="search" id="form1" class="form-control" v-model="pesquisa" placeholder="Pesquisar Empresa" />
      </div>
      <button onclick="window.location.reload()" type="button" class="btn btn-dark ml-2">
        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-search"
          viewBox="0 0 16 16">
          <path fill-rule="evenodd" d="M8 3a5 5 0 1 0 4.546 2.914.5.5 0 0 1 .908-.417A6 6 0 1 1 8 2v1z" />
          <path
            d="M8 4.466V.534a.25.25 0 0 1 .41-.192l2.36 1.966c.12.1.12.284 0 .384L8.41 4.658A.25.25 0 0 1 8 4.466z" />
        </svg>
      </button>

      <button @click="exportPdf" type="submit" required="required" class="btn btn-dark imprimir ">
        IMPRIMIR
      </button>
    </div>

    <div class="container">
      <table class="content-table table">
        <thead class="table-dark">
          <tr>
            <th>Id</th>
            <th>Nome</th>
            <th>Nome Empresa</th>
            <th>Data Última Refeição</th>
            <th>Total de Refeições</th>
            <th></th>
          </tr>
        </thead>

        <tbody v-for="colaborador in colaboradoresFiltrados" :key="colaborador.id">
          <tr>
            <td>{{ colaborador.id }}</td>
            <td>{{ colaborador.nome }}</td>
            <td>{{ colaborador.nome_empresa }}</td>
          </tr>


        </tbody>

      </table>

    </div>
  </main>
</template>



<script>

import jsPDF from 'jspdf'
import 'jspdf-autotable'


export default {
  data: () => ({
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
        colaborador.nome_empresa.toLowerCase().includes(this.pesquisa.toLowerCase())
      )
    },
  },
  methods: {
    exportPdf() {

      console.log(this.colaboradoresFiltrados)
      const vm = this
      const columns = [
        { title: "Id", dataKey: "id" },
        { title: "Nome", dataKey: "nome" },
        { title: "Empresa", dataKey: "nome_empresa" },
        { title: "Data Última Refeição", dataKey: "calvalcante" },
        { title: "Total de Refeições", dataKey: "" }

      ];
      const doc = jsPDF('p', 'pt');
      doc.text('Relatório Geral', 30, 20)
      doc.autoTable(columns, vm.colaboradoresFiltrados,
        {
          theme: "grid"
        });
      doc.save('Relatório Geral .pdf');
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

.btn-dark {
  background-color: #009879;
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

.imprimir {
  margin-left: 1%;
}
</style>
