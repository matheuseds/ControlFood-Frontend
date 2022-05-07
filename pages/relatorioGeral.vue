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

 

    <div class="row">
      <div >
        <button type="button" class="btn btn-dark botao">Imprimir</button>
        <div class="row">
        <b-dropdown
          id="dropdown-1"
          text="Empresas"
          class="m-md-2 dropdown"
          variant="dark"
        >
          <b-dropdown-item>Empresa 1</b-dropdown-item>
          <b-dropdown-item>Empresa 2</b-dropdown-item>
          <b-dropdown-item>Empresa 3</b-dropdown-item>
         
        </b-dropdown>
      </div>
      </div>
      
    </div>

    <div class="container">
      <table class="table">
        <thead class="table-dark">
          <tr>
            <th>Id</th>
            <th>Nome</th>
            <th>Nome Empresa</th>
            <th>CPF</th>
            <th>Total de Refeições</th>
          </tr>
        </thead>

        <tbody v-for="relatorio in relatorios" :key="relatorio.id">
          <tr>
            <td >{{relatorio.id}}</td>
            <td >{{relatorio.nome}}</td>
            <td >{{relatorio.empresa}}</td>
            <td >{{relatorio.CPF}}</td>
            <td >{{relatorio.refeicoes}}</td>
          </tr>
       
     
          
        </tbody>
      </table>
    </div>
  </main>
</template>

<script>
export default {
   data: () => ({
    relatorios: [
      {
        id: 1,
        nome: 'Nome',
        empresa: 'Empresa',
        CPF: '303.810.860-03',
        refeicoes:'20',
      },
      {
        id: 2,
        nome: 'Nome',
        empresa: 'Empresa',
        CPF: '303.810.860-03',
        refeicoes:'20',
      },
    ],
  }),
}
</script>

<style>

.botao{
 width: 110%;
}

.dropdown {
  margin-bottom: 10% !important;
  width: 84%;
  }
</style>