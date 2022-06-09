<template>
  <main>
    <div class="form-signin main">
      <div class="card mt-n2">
        <div class="card-body mt-n1 ajustes">
          <form @submit.prevent="cadastro">
            <h1>Cadastre-se</h1>
            <b-alert :variant="responseColor" :show="showAlert">{{
              responseMessage
            }}</b-alert>

            <div class="form-group">
              <input
                v-model="usuario.nome"
                type="text"
                required
                class="form-control-2 form-control"
                placeholder="Usuário"
              />
            </div>
            <div class="form-group">
              <input
                v-model="usuario.email"
                type="email"
                required
                class="form-control-2 form-control"
                placeholder="Email"
              />
            </div>

            <div class="form-group">

              <input
                v-model="usuario.senha"
                :type="filedType"
                required
                class="form-control-2 form-control"
                placeholder="Password"
              />

              <h6 class="senha" @click="hideShow">Mostrar senha</h6>
            </div>

            <b-button class="w-100 btn btn-lg btn-v" type="submit"
              >Cadastrar</b-button
            >
            <b-button class="w-100 btn btn-lg btn-v" href="\"
              >Acessar login</b-button
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
* {
  font-family: sans-serif;
}

.btn-v{
   background-color:#e42021;
   padding: 10px 3%;
   border-radius: 100px;
   color: white;
   transition:0.2s;
   float: right;
   font-family: "WorkSansSemiBold";
   border: none;
   font-size: 18px;
   margin: 5px;
}
.btn-v:hover{
  color: white;
  background-color: #fc8585;
  
}
h1{ 
  font-family: "WorkSansSemiBold";
  text-align: center;
  }
.mt-n2 {
  display: flex;

  align-items: center;
  justify-content: center;

  box-shadow: none;
  border: 0;
}

.senha {
  cursor: pointer;
  padding-top: 10px;
  text-align: right;
}

.botao {
  width: 6rem;
  min-width: 180px;
  max-width: 800px;
  margin-top: 2%;
}
.ajustes {
  margin-left: auto;
  margin-right: auto;
  margin-top: 9% !important;
}
.form-control-2 {
  width:100% !important;
  color: #333030;
  background-color: #fff;
  border-bottom: 1px solid #333030 !important;
  border: 0px solid;
  border-radius: 0;
  margin: 10px 0px;
  font-family: "WorkSansRegular";
  font-size: 20px;
}
.form-control-2:focus{
  background: #e2e2e2;
   border: none !important;
}
/* geral*/
@font-face {
  font-family: "WorkSansRegular";
  src: url("fontes/WorkSans-Regular.ttf");
}
@font-face {
  font-family: "WorkSansMedium";
  src: url("fontes/WorkSans-Medium.ttf");
}
@font-face {
  font-family: "WorkSansSemiBold";
  src: url("fontes/WorkSans-SemiBold.ttf");
}
@font-face {
  font-family: "WorkSansBold";
  src: url("fontes/WorkSans-Bold.ttf");
}
</style>
