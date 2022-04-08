<template>
  <main>
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
            <NuxtLink to="/relatorioGeral" class="nav-link"
              >Relatorios</NuxtLink
            >
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

        <tbody>
          <tr>
            <td>0001</td>
            <td>Nome</td>
            <td>Nome Empresa</td>
            <td>303.810.860-03</td>
            <td>20</td>
          </tr>
          <tr>
            <td>0002</td>
            <td>Nome</td>
            <td>Nome Empresa</td>
            <td>303.810.860-03</td>
            <td>20</td>
          </tr>
          <tr>
            <td>0003</td>
            <td>Nome</td>
            <td>Nome Empresa</td>
            <td>303.810.860-03</td>
            <td>20</td>
          </tr>
          <tr>
            <td>0004</td>
            <td>Nome</td>
            <td>Nome Empresa</td>
            <td>303.810.860-03</td>
            <td>20</td>
          </tr>
          <tr>
            <td>0005</td>
            <td>Nome</td>
            <td>Nome Empresa</td>
            <td>303.810.860-03</td>
            <td>20</td>
          </tr>
          <tr>
            <td>0006</td>
            <td>Nome</td>
            <td>Nome Empresa</td>
            <td>303.810.860-03</td>
            <td>20</td>
          </tr>
          <tr>
            <td>0007</td>
            <td>Nome</td>
            <td>Nome Empresa</td>
            <td>303.810.860-03</td>
            <td>20</td>
          </tr>
          <tr>
            <td>0008</td>
            <td>Nome</td>
            <td>Nome Empresa</td>
            <td>303.810.860-03</td>
            <td>20</td>
          </tr>
        </tbody>
      </table>
    </div>
  </main>
</template>

<script>
export default {}
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

.icons {
  margin-left: 38%;
}

.dropdown {
  margin-bottom: 10% !important;
  width: 84%;
  }
</style>