<template>
  <main>
    <div class="form-signin main">
      <div class="card">
        <div class="card-body mt-n1 ajustes">
          <form @submit.prevent="cadastro">
            <h2 class="h3 mb-3 fw-normal text-center corTexto">Cadastre-se</h2>
            <b-alert :variant="responseColor" :show="showAlert">{{
              responseMessage
            }}</b-alert>

            <div class="form-group">
              <label class="corTexto">Usuário</label>
              <input
                v-model="usuario.nome"
                type="text"
                required
                class="form-control form-control-lg"
                placeholder="Usuário"
              />
            </div>
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

                <h6 class="senha" @click="hideShow">
                 Mostrar senha
                </h6>
              
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
    filedType: 'password',
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
    hideShow() {
      this.filedType = this.filedType === 'password' ? 'text' : 'password'
    },

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
        this.responseMessage =
          'A senha deve conter 8 dígitos, 1 caracter maiúsculo e um caracter especial'
        this.showAlert = true
      }
    },
  },
}
</script>

<style>
.senha{
  cursor: pointer;
  padding-top: 10px;
  text-align: right;
}

.botao {
  width: 6rem;
  min-width: 320px;
  max-width: 800px;
  margin-top: 2%;
}
.ajustes {
  margin-left: auto;
  margin-right: auto;
  margin-top: 9% !important;
}
</style>
