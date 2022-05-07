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
            <NuxtLink to="/cadastrarEmpresa" class="nav-link" >Cadastrar Empresas</NuxtLink>
          </li>
          <li class="nav-item active">
            <NuxtLink to="/cadastrarColaborador" class="nav-link" >Cadastrar Colaborador</NuxtLink>
          </li>
          <li class="nav-item active">
            <NuxtLink to="/listarColaboradores" class="nav-link" >Listar Colaboradores</NuxtLink>
          </li>
           <li class="nav-item active">
            <NuxtLink to="/listarEmpresas" class="nav-link" >Listar Empresas</NuxtLink>
          </li>
          <li class="nav-item active">
            <NuxtLink to="/relatorioGeral" class="nav-link" >Relatorios</NuxtLink>
          </li>
        </ul>
      </div>
    </nav>

    <div class="container input-group pesquisa">
      <div class="pesquisa">
        <input type="search" id="form1" class="form-control" />
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
          <tr >
            <th>Id</th>
            <th>CNPJ</th>
            <th>Empresa</th>
            <th>Contato do Responsável</th>
            <th>E-mail</th>
            <th>Endereço</th>
            <th>Número</th>
          </tr>
        </thead>

        <tbody>
          <tr v-for="lista in listas" :key="lista.id">
            <td>{{lista.id}}</td>
            <td>{{lista.CNPJ }}</td>
            <td>{{lista.empresa }}</td>
            <td>{{lista.contatoresponsavel }}</td>
            <td>{{lista.email }}</td>
            <td>{{lista.endereco }}</td>
            <td>{{lista.numero }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </main>
</template>

<script>
export default {
  data: () => ({
    listas: [
      {
        id: 1,
        CNPJ: '39.299.702/0001-53',
        empresa: 'Empresa',
        contatoresponsavel: 'marthe3347@hotmail.com',
        email: 'marthe3347@uorak.com',
        endereco: 'rua major gote',
        numero: 140,
      },
       {
        id: 2,
        CNPJ: '39.299.702/0001-53',
        empresa: 'Empresa',
        contatoresponsavel: 'marthe3347@hotmail.com',
        email: 'marthe3347@uorak.com',
        endereco: 'rua major gote',
        numero: 140,
      },
    ],
  }),
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