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
    <svg xmlns="http://www.w3.org/2000/svg" width="60" height="40" fill="currentColor" class="bi bi-briefcase-fill icons" viewBox="0 0 16 16">
  <path d="M6.5 1A1.5 1.5 0 0 0 5 2.5V3H1.5A1.5 1.5 0 0 0 0 4.5v1.384l7.614 2.03a1.5 1.5 0 0 0 .772 0L16 5.884V4.5A1.5 1.5 0 0 0 14.5 3H11v-.5A1.5 1.5 0 0 0 9.5 1h-3zm0 1h3a.5.5 0 0 1 .5.5V3H6v-.5a.5.5 0 0 1 .5-.5z"/>
  <path d="M0 12.5A1.5 1.5 0 0 0 1.5 14h13a1.5 1.5 0 0 0 1.5-1.5V6.85L8.129 8.947a.5.5 0 0 1-.258 0L0 6.85v5.65z"/>
</svg>
    <p class="card-text">3949</p>
  </div>
</div>

<div class="card" style="width: 17rem;">
 
  <div class="card-body">
    <h5 class="card-title"> Total de Colaboradores</h5>
    <svg xmlns="http://www.w3.org/2000/svg" width="60" height="40" fill="currentColor" class="bi bi-person-check-fill icons" viewBox="0 0 16 16">
  <path fill-rule="evenodd" d="M15.854 5.146a.5.5 0 0 1 0 .708l-3 3a.5.5 0 0 1-.708 0l-1.5-1.5a.5.5 0 0 1 .708-.708L12.5 7.793l2.646-2.647a.5.5 0 0 1 .708 0z"/>
  <path d="M1 14s-1 0-1-1 1-4 6-4 6 3 6 4-1 1-1 1H1zm5-6a3 3 0 1 0 0-6 3 3 0 0 0 0 6z"/>
</svg>
    <p class="card-text">3434</p>
    
  </div>
</div>

<div class="card" style="width: 17rem;">
  
  <div class="card-body">
    <h5 class="card-title">Quantidade de Refeições</h5>
    <svg xmlns="http://www.w3.org/2000/svg" width="60" height="40" fill="currentColor" class="bi bi-cart4 icons" viewBox="0 0 16 16">
  <path d="M0 2.5A.5.5 0 0 1 .5 2H2a.5.5 0 0 1 .485.379L2.89 4H14.5a.5.5 0 0 1 .485.621l-1.5 6A.5.5 0 0 1 13 11H4a.5.5 0 0 1-.485-.379L1.61 3H.5a.5.5 0 0 1-.5-.5zM3.14 5l.5 2H5V5H3.14zM6 5v2h2V5H6zm3 0v2h2V5H9zm3 0v2h1.36l.5-2H12zm1.11 3H12v2h.61l.5-2zM11 8H9v2h2V8zM8 8H6v2h2V8zM5 8H3.89l.5 2H5V8zm0 5a1 1 0 1 0 0 2 1 1 0 0 0 0-2zm-2 1a2 2 0 1 1 4 0 2 2 0 0 1-4 0zm9-1a1 1 0 1 0 0 2 1 1 0 0 0 0-2zm-2 1a2 2 0 1 1 4 0 2 2 0 0 1-4 0z"/>
</svg>
    <p class="card-text">3430</p>
    
  </div>
</div>
</div>


<div class="input-group pesquisa">
  <div class="pesquisa">
    <input type="search" id="form1" class="form-control" />
  </div>
  <button type="button" class="btn btn-dark">
    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-search" viewBox="0 0 16 16">
  <path d="M11.742 10.344a6.5 6.5 0 1 0-1.397 1.398h-.001c.03.04.062.078.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1.007 1.007 0 0 0-.115-.1zM12 6.5a5.5 5.5 0 1 1-11 0 5.5 5.5 0 0 1 11 0z"/>
</svg>
  </button>
</div>


<h1 class="titulo">Recentes</h1>
<div class="container">
<table class="table">

    <thead class="table-dark">
        <tr>
            <th>#</th>
            <th>Nome</th>
            <th>Data</th>
            <th>Hora</th>
        </tr>
    </thead>

    <tbody>
       <tr>
           <td>0001</td>
           <td>Nome</td>
           <td>28/03/2022</td>
           <td>13:26</td>
       </tr>
       <tr>
        <td>0002</td>
        <td>Nome</td>
        <td>28/03/2022</td>
        <td> 13:26</td>
      </tr>
      <tr>
        <td>0003</td>
        <td>Nome</td>
        <td>28/03/2022</td>
        <td> 13:26</td>
      </tr>
        <tr>
           <td>0004</td>
           <td>Nome</td>
           <td>28/03/2022</td>
           <td>13:26</td>
       </tr>
       <tr>
        <td>0005</td>
        <td>Nome</td>
        <td>28/03/2022</td>
        <td> 13:26</td>
      </tr>
      <tr>
        <td>0006</td>
        <td>Nome</td>
        <td>28/03/2022</td>
        <td> 13:26</td>
      </tr>
        <tr>
           <td>0007</td>
           <td>Nome</td>
           <td>28/03/2022</td>
           <td>13:26</td>
       </tr>
       <tr>
        <td>0008</td>
        <td>Nome</td>
        <td>28/03/2022</td>
        <td> 13:26</td>
      </tr>
    
      
    </tbody>

 </table>
</div>

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

  .icons{
    margin-left: 38%;
  }
     
  .card-text{
    text-align: center;
    font-weight: bold;
  }
 
</style>