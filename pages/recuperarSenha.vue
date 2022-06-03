<template>
  <main class="form-signin main">
    <div class="card">
      <div class="card-body mt-n1">
        <form @submit.prevent="login">
          <h2 class="h3 mb-3 fw-normal text-center corTexto">
            Recuperar Senha
          </h2>

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
            <label class="corTexto">Nova senha</label>
            <input
              v-model="usuario.senha"
              type="password"
              required
              class="form-control form-control-lg"
              placeholder="Password"
            />
          </div>

          <b-button class="w-100 btn btn-lg btn-dark botao" type="submit"
            >Confirmar</b-button
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
    filedType: 'password',
    usuario: {
      email: '',
      senha: '',
    },
  }),
  
}
</script>

<style>

* {
  font-family: sans-serif; 
}

.recuperarsenha {
  cursor: pointer;
  padding-top: 10px;
  justify-content: center;
  display: block;
  float: right;
}

.mt-n1 {
  margin-left: auto !important;
  margin-right: auto !important;
  margin-top: 15% !important;
}
</style>