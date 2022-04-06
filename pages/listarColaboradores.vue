<template>
  <main>
   <nav class="navbar navbar-expand navbar-dark bg-dark">
     <NuxtLink to="/dashboardSite" class="navbar-brand" >Control Food</NuxtLink>

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

    <h1 class="titulo">Colaboradores Cadastrados</h1>
    <div class="container">
      <table class="table">
        <thead class="table-dark">
          <tr>
            <th>#</th>
            <th>Nome</th>
            <th>CPF</th>
            <th>Empresa</th>
            <th>E-mail</th>
            <th>Nº Matricula</th>
          </tr>
        </thead>

        <tbody>
          <tr>
            <td>0001</td>
            <td>Nome</td>
            <td>34549689501</td>
            <td>Empresa</td>
            <td>28/03/2022</td>
            <td>123454356</td>
          </tr>
          <tr>
            <td>0002</td>
            <td>Nome</td>
            <td>34549689501</td>
            <td>Empresa</td>
            <td>marthe3347@uorak.com</td>
            <td>123454356</td>
          </tr>
          <tr>
            <td>0003</td>
            <td>Nome</td>
            <td>34549689501</td>
            <td>Empresa</td>
            <td>marthe3347@uorak.com</td>
            <td>123454356</td>
          </tr>
          <tr>
            <td>0004</td>
            <td>Nome</td>
            <td>34549689501</td>
            <td>Empresa</td>
            <td>marthe3347@uorak.com</td>
            <td>123454356</td>
          </tr>
          <tr>
            <td>0005</td>
            <td>Nome</td>
            <td>34549689501</td>
            <td>Empresa</td>
            <td>marthe3347@uorak.com</td>
            <td>123454356</td>
          </tr>
          <tr>
            <td>0006</td>
            <td>Nome</td>
            <td>34549689501</td>
            <td>Empresa</td>
            <td>marthe3347@uorak.com</td>
            <td>123454356</td>
          </tr>
          <tr>
            <td>0007</td>
            <td>Nome</td>
            <td>34549689501</td>
            <td>Empresa</td>
            <td>marthe3347@uorak.com</td>
            <td>123454356</td>
          </tr>
          <tr>
            <td>0008</td>
            <td>Nome</td>
            <td>34549689501</td>
            <td>Empresa</td>
            <td>marthe3347@uorak.com</td>
            <td>123454356</td>
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
.card {
  display: inline-block;
  margin-top: 2%;
  margin-left: 5%;
  margin-right: 5%;
  box-shadow: 1px 3px 3px rgba(0, 0, 0, 0.459);
}

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

.icons {
  margin-left: 38%;
}

.card-text {
  text-align: center;
  font-weight: bold;
}
</style>