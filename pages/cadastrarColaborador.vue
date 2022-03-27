<template>
  <main>
    <nav class="navbar navbar-expand navbar-dark bg-dark">
      <a class="navbar-brand" href="#">Control Food</a>
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
            <a class="nav-link" href="#"
              >Cadastrar Empresa <span class="sr-only">(current)</span></a
            >
          </li>
          <li class="nav-item active">
            <a class="nav-link" href="#"
              >Cadastrar Colaborador <span class="sr-only">(current)</span></a
            >
          </li>
          <li class="nav-item active">
            <a class="nav-link" href="#"
              >Relatório <span class="sr-only">(current)</span></a
            >
          </li>
        </ul>
      </div>
    </nav>
    <div class="container">
      <div class="row">
        <div class="col-6">
          <div class="card">
            <div class="card-body">
              <h1>Cadastrar Colaboradores</h1>
              <form id="form-contato">
                <div class="form-group">
                  <label for="email">Nome:</label>
                  <input
                    class="form-control"
                    type="text"
                    name="nome"
                    id="nomeColaborador"
                    placeholder="Nome"
                    required
                  />
                </div>
                <div class="form-group">
                  <label for="text">CPF:</label>
                  <input
                    class="form-control"
                    type="text"
                    name="email"
                    id="emailColaborador"
                    placeholder="E-mail"
                    required
                  />
                </div>

                <div class="form-group">
                  <label for="email">Nome da Empresa:</label>
                  <input
                    class="form-control"
                    type="text"
                    name="nome"
                    id="nomeEmpresa"
                    placeholder="Nome da Empresa"
                    required
                  />
                </div>
                <div class="form-group">
                  <label for="email">E-mail:</label>
                  <input
                    class="form-control"
                    type="email"
                    name="email"
                    id="emailColaborador"
                    placeholder="E-mail"
                    required
                  />
                </div>
                <div class="form-group">
                  <label for="email">Número de Matricula:</label>
                  <input
                    class="form-control"
                    type="text"
                    name="nome"
                    id="matriculaColaborador"
                    placeholder="Número da Matricula"
                    required
                  />
                </div>
                <div class="custom-file">
                  <input type="file" class="custom-file-input" id="foto" />
                  <label class="custom-file-label" for="customFile"
                    >Enviar Foto</label
                  >
                </div>
                <div class="form-group text-center botao">
                  <button type="submit" class="btn btn-primary" required>ENVIAR</button>
                </div>
                
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  data: () => ({
    email: '',
    password: '',
  }),

  methods: {
    login() {
      alert('login')
    },
  },
}
</script>

<style>

.botao{
    margin-top: 3%;
}
.row{
    margin-top: 5%;
    justify-content: center;
}
</style>