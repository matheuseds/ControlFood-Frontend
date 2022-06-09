<template>
  <main class="form-signin main">
    <div class="card mt-n2">
      <div class="mt-n1">
        <form @submit.prevent="login">
          <h1>Autenticação de duplo fator</h1>

          <div class="form-group">
            <input placeholder="Insira o token"
              v-model="usuario.token"
              required
              class="form-control-2 form-control"
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

.btn-dark{
   background-color: #e42021;
   font-family: "WorkSansSemiBold";
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