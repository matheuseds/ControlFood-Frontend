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

        <tbody
          v-for="colaborador in colaboradoresFiltrados"
          :key="colaborador.id"
        >
          <tr>
            <td>{{ colaborador.id }}</td>
            <td>{{ colaborador.nome }}</td>
            <td>{{ colaborador.cpf }}</td>
            <td>{{ colaborador.nome_empresa }}</td>
            <td>{{ colaborador.email }}  </td>
           <td>
             <button><svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" fill="currentColor" class="bi bi-trash-fill" viewBox="0 0 16 16">
  <path d="M2.5 1a1 1 0 0 0-1 1v1a1 1 0 0 0 1 1H3v9a2 2 0 0 0 2 2h6a2 2 0 0 0 2-2V4h.5a1 1 0 0 0 1-1V2a1 1 0 0 0-1-1H10a1 1 0 0 0-1-1H7a1 1 0 0 0-1 1H2.5zm3 4a.5.5 0 0 1 .5.5v7a.5.5 0 0 1-1 0v-7a.5.5 0 0 1 .5-.5zM8 5a.5.5 0 0 1 .5.5v7a.5.5 0 0 1-1 0v-7A.5.5 0 0 1 8 5zm3 .5v7a.5.5 0 0 1-1 0v-7a.5.5 0 0 1 1 0z"/>
</svg></button> <button><svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" fill="currentColor" class="bi bi-pencil-square" viewBox="0 0 16 16">
  <path d="M15.502 1.94a.5.5 0 0 1 0 .706L14.459 3.69l-2-2L13.502.646a.5.5 0 0 1 .707 0l1.293 1.293zm-1.75 2.456-2-2L4.939 9.21a.5.5 0 0 0-.121.196l-.805 2.414a.25.25 0 0 0 .316.316l2.414-.805a.5.5 0 0 0 .196-.12l6.813-6.814z"/>
  <path fill-rule="evenodd" d="M1 13.5A1.5 1.5 0 0 0 2.5 15h11a1.5 1.5 0 0 0 1.5-1.5v-6a.5.5 0 0 0-1 0v6a.5.5 0 0 1-.5.5h-11a.5.5 0 0 1-.5-.5v-11a.5.5 0 0 1 .5-.5H9a.5.5 0 0 0 0-1H2.5A1.5 1.5 0 0 0 1 2.5v11z"/>
</svg></button>
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
