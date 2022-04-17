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
              >Listar Colaboradores<span class="sr-only">(current)</span></a
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
              <h1>Cadastrar Empresa</h1>
              <form @submit.prevent="cadastro" id="form-contato">
                <b-alert :variant="responseColor" :show="showAlert">{{
                  responseMessage
                }}</b-alert>

                <div>
               <label for="nome">CNPJ:</label>
                  <input
                    v-model="empresa.cnpj"
                    class="form-control"
                    type="text"
                    name="nome"
                    id="cnpj"
                    placeholder="CNPJ"
                    v-maska="'##.###.###/####-##'"
                    required
                  />
                </div>
                <div class="form-group">
                  <label for="email">Nome da empresa:</label>
                  <input
                    v-model="empresa.nomeEmpresa"
                    class="form-control"
                    type="text"
                    placeholder="Nome da Empresa"
                    required
                  />
                </div>
                <div class="form-group">
                  <label for="email">E-mail:</label>
                  <input
                    v-model="empresa.email"
                    class="form-control"
                    type="email"
                    placeholder="E-mail"
                    required
                  />
                </div>
                <div class="form-group">
                  <label for="email">Nome do Responsável:</label>
                  <input
                    v-model="empresa.nomeResponsavel"
                    class="form-control"
                    type="text"
                    placeholder="Nome da Empresa"
                    required
                  />
                </div>
                <div class="form-group">
                  <label for="email">Contato do Responsável:</label>
                  <input
                    v-model="empresa.contatoResponsavel"
                    class="form-control"
                    type="text"
                    placeholder="Contato do Responsável"
                    required
                  />
                </div>
                <div class="form-group">
                  <label for="inputAddress">Endereço</label>
                  <input
                    v-model="empresa.endereco"
                    type="text"
                    class="form-control"
                    placeholder="Rua Major Gote, n° 808"
                    required
                  />
                </div>
                <div class="form-row">
                  <div class="form-group col-md-6">
                    <label for="inputCity">Cidade</label>
                    <input
                      v-model="empresa.cidade"
                      type="text"
                      class="form-control"
                      placeholder="Patos de Minas"
                      required
                    />
                  </div>
                <div class="form-group col-md-3">
                    <label for="inputEstado">Estado</label>
                    <input
                    v-model="empresa.estado"
                      type="text"
                      class="form-control"
                      id="estado"
                      placeholder="MG"
                      v-maska="'AA'"
                      required
                    />
                  </div>
                 
                </div>

                <div class="form-group text-center">
                  <button type="submit" class="btn btn-dark">ENVIAR</button>
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
    empresa: {
      cnpj: '',
      nomeEmpresa: '',
      email: '',
      nomeResponsavel: '',
      contatoResponsavel: '',
      endereco: '',
      cidade: '',
      estado: '',
      cep: '',
    },
    responseColor: null,
    responseMessage: null,
    showAlert: false,
  }),

  methods: {
    async cadastro() {
      /**
       * Post = Enviar dados
       * Get = Receber dados
       * Patch = Atualizar dados
       * Delete = Excluir dados
       */
      try {
        const response = await this.$axios.$post('/empresa', this.empresa)
        this.responseColor = 'success'
        this.responseMessage = response.message
        this.showAlert = true
      } catch (error) {
        this.responseColor = 'danger'
        this.responseMessage = 'Ocorreu um erro'
        this.showAlert = true
      }
    },
  },
}
</script>

<style>
.row {
  margin-top: 3%;
  justify-content: center;
}
</style>
