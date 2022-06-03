<template>
  <main class="form-signin main">
    <div class="card">
      <div class="card-body mt-n1">
        <form @submit.prevent="login">
          <h2 class="h3 mb-3 fw-normal text-center corTexto">Faça o Login</h2>

          <div class="form-group">
            <label class="corTexto">Email</label>
            <input
              v-model="usuario.email"
              type="email"
              required
              class="form-control form-control-lg"
              placeholder="Email"
            />
          </div>

          <div class="form-group">
            <label class="corTexto">Senha</label>
            <input
              v-model="usuario.senha"
              type="password"
              required
              class="form-control form-control-lg"
              placeholder="Password"
            />
          </div>

          <b-button class="w-100 btn btn-lg btn-dark botao" type="submit"
            >Entrar</b-button
          >
          <b-button class="w-100 btn btn-lg btn-dark botao">Cadastrar</b-button>

          <NuxtLink to="/recuperarSenha" class="recuperarsenha"
            >Recuperar senha</NuxtLink
          >
        </form>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  name: 'IndexPage',
  data: () => ({
    usuario: {
      email: '',
      senha: '',
    },
  }),

  methods: {
    async login() {
      try {
        await this.$axios.$post('/usuario/login', this.usuario)
        this.$router.push({ name: 'dashboardSite' })
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

* {
  font-family: sans-serif; 
}

.btn-dark{
  background-color:#009879;
}

.recuperarsenha {
  cursor: pointer;
  padding-top: 10px;
  text-align: right;
}

.botao {
  width: 6rem !important;
  min-width: 49% !important;
  margin-top: 2% !important;
}
.mt-n1 {
  margin-left: auto !important;
  margin-right: auto !important;
  margin-top: 15% !important;
}
</style>
