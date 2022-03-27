<template>
  <main >
<nav class="navbar navbar-expand navbar-dark bg-dark">
      <a class="navbar-brand" href="#">Control Food</a>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarsExample02" aria-controls="navbarsExample02" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarsExample02">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item active">
            <a class="nav-link" href="#">Cadastrar Empresa <span class="sr-only">(current)</span></a>
          </li>
          <li class="nav-item active">
            <a class="nav-link" href="#">Cadastrar Colaborador <span class="sr-only">(current)</span></a>
          </li>
          <li class="nav-item active">
            <a class="nav-link" href="#">Relatório <span class="sr-only">(current)</span></a>
          </li>
        </ul>
        
      </div>
    </nav>
<div class="row">
      
<div class="card" style="width: 17rem;">
 
  <div class="card-body">
    <h5 class="card-title">Empresas Cadastradas</h5>
    <p class="card-text">3949</p>
  </div>
</div>

<div class="card" style="width: 17rem;">
 
  <div class="card-body">
    <h5 class="card-title"> Total de Colaboradores</h5>
    <p class="card-text">3434</p>
    
  </div>
</div>

<div class="card" style="width: 17rem;">
  
  <div class="card-body">
    <h5 class="card-title">Quantidade de Refeições</h5>
    <p class="card-text">343</p>
    
  </div>
</div>
</div>


<div class="input-group pesquisa">
  <div class="pesquisa">
    <input type="search" id="form1" class="form-control" />
  </div>
  <button type="button" class="btn btn-primary">
    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-search" viewBox="0 0 16 16">
  <path d="M11.742 10.344a6.5 6.5 0 1 0-1.397 1.398h-.001c.03.04.062.078.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1.007 1.007 0 0 0-.115-.1zM12 6.5a5.5 5.5 0 1 1-11 0 5.5 5.5 0 0 1 11 0z"/>
</svg>
  </button>
</div>


<h1 class="titulo">Recentes</h1>

<table class="table">
  <thead>
    <tr>
      <th scope="col">#</th>
      <th scope="col">Nome</th>
      <th scope="col">Data</th>
      <th scope="col">Hora</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">1</th>
      <td>Mark</td>
      <td>27/03/2022</td>
      <td>00:39</td>
    </tr>
    <tr>
      <th scope="row">2</th>
      <td>Jacob</td>
      <td>27/03/2022</td>
      <td>00:39</td>
    </tr>
    <tr>
       <tr>
      <th scope="row">3</th>
      <td>Mark</td>
      <td>27/03/2022</td>
      <td>00:39</td>
    </tr>
    <tr>
      <th scope="row">4</th>
      <td>Jacob</td>
      <td>27/03/2022</td>
      <td>00:39</td>
    </tr>
    <tr>
       <tr>
      <th scope="row">5</th>
      <td>Mark</td>
      <td>27/03/2022</td>
      <td>00:39</td>
    </tr>
    <tr>
      <th scope="row">6</th>
      <td>Jacob</td>
      <td>27/03/2022</td>
      <td>00:39</td>
    </tr>
   
    

  </tbody>
</table>


  </main>
</template>

<script>
export default {

}
</script>

<style>  
 
    .card{
      display: inline-block;
      margin-top: 2%;
      margin-left: 5%;
      margin-right: 5%;
     
    }
    .titulo{
      margin-top: 2%;
     text-align: center;
      margin-bottom: 3%;

    }
    .pesquisa{
      align-items: center;
      margin-left: 20%;
      margin-top: 2%;
      width: 60% ;
    }
    .form-control{
      margin-bottom: 3%;
      
    }
    .row {
  justify-content: center;
}
     
 
</style>