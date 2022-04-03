<template>
  <main>
    <div class="form-signin main">
      <div class="card">
        <div class="card-body mt-n1">
          <form @submit.prevent="cadastro">
            <h2 class="h3 mb-3 fw-normal text-center">Cadastre-se</h2>
            <b-alert :variant="responseColor" :show="showAlert">{{
              responseMessage
            }}</b-alert>

            <div class="form-group">
              <label>Usuário</label>
              <input
                v-model="usuario.nome"
                type="text"
                required
                class="form-control form-control-lg"
                placeholder="Usuário"
              />
            </div>
            <div class="form-group">
              <label>Email</label>
              <input
                v-model="usuario.email"
                type="email"
                required
                class="form-control form-control-lg"
                placeholder="Email"
              />
            </div>

            <div class="form-group">
              <label>Senha</label>
              <input
                v-model="usuario.senha"
                type="password"
                required
                class="form-control form-control-lg"
                placeholder="Password"
              />
            </div>

            <b-button class="w-100 btn btn-lg btn-dark botao" type="submit"
              >Cadastrar</b-button
            >
          </form>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  data: () => ({
    usuario: {
      nome: '',
      email: '',
      senha: '',
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
        const response = await this.$axios.$post('/usuario', this.usuario)
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
.main {
  width: 100vw;
}
.botao {
  width: 6rem !important;
  min-width: 320px !important;
  max-width: 800px !important;
  margin-top: 2% !important;
}
.mt-n1 {
  margin-left: auto !important;
  margin-right: auto !important;
  margin-top: 14% !important;
  min-width: 320px !important;
  max-width: 800px !important;
}
.senha {
  margin-top: 7% !important;
}
</style>
