<template>
  <main class="form-signin main">
    <div class="card mt-n2">
      <div class="card-body mt-n1">
        <form @submit.prevent="login">
          <h2 class="h3 mb-3 fw-normal text-center corTexto">Faça o Login</h2>

          <b-alert :variant="responseColor" :show="showAlert">{{
            responseMessage
          }}</b-alert>

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
              :type="filedType"
              required
              class="form-control form-control-lg"
              placeholder="Password"
            />

            <h6 class="senha" @click="hideShow2">Mostrar senha</h6>
          </div>

          <b-button class="w-100 btn btn-lg btn-dark botao" type="submit"
            >Entrar</b-button
          >

          <b-button href="\CadastrarUsuario" class="w-100 btn btn-lg btn-dark botao" >Cadastrar</b-button>
        </form>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  name: 'IndexPage',
  data: () => ({
    filedType: 'password',
    usuario: {
      email: '',
      senha: '',
    },
    responseColor: null,
    responseMessage: null,
    showAlert: false,
  }),

  methods: {
    async login() {
      try {
        await this.$axios.$post('/usuario/login', this.usuario)
        // localStorage.setItem('token', response.token)
        // localStorage.setItem('id', response.id)
        this.$router.push({ name: 'duploFator' })
      } catch (error) {
        this.responseColor = 'danger'
        this.responseMessage = 'Ocorreu um erro'
        this.showAlert = true
      }
    },
    hideShow2() {
      this.filedType = this.filedType === 'password' ? 'text' : 'password'
    },
  },
}
</script>

<style>
* {
  font-family: sans-serif;
}

.btn-dark {
  background-color: #009879;
}

.senha {
  cursor: pointer;
  padding-top: 10px;
  text-align: right;
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

.mt-n2 {
  display: flex;

  align-items: center;
  justify-content: center;

  box-shadow: none;
  border: 0;
}
.mt-n1 {
  margin-left: auto !important;
  margin-right: auto !important;
  margin-top: 15% !important;
}
</style>
