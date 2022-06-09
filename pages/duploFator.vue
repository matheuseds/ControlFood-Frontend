<template>
  <main class="form-signin main">
    <div class="card mt-n2">
      <div class="card-body mt-n1">
        <form @submit.prevent="login">
          <h2 class="h3 mb-3 fw-normal text-center corTexto title"> Foi enviado um código para <br> seu e-mail</h2>
          <div class="form-group">
            <label class="corTexto">Token</label>
            <input
              v-model="usuario.token"
              required
              class="form-control form-control-lg"
            />
          </div>
          <b-button class="w-100 btn btn-lg btn-dark botao" type="submit"
            >Entrar</b-button
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
    token: ''
    },
  }),

  methods: {
     login() {
      try { 
         localStorage.setItem('token', this.usuario.token)
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

.title{
font-size: 26px;
}

.btn-dark{
  background-color:#009879;
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