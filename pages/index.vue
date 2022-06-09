<template>
  <main class="form-signin main">
    <div class=" mt-n2">
      <div class="mt-n1" style="width: 50%;">
        <form @submit.prevent="login">
           <div style="text-align: center; margin: 4% 0;">
                <b-img
                  class="img-menu"
                  src="https://designerelite.com.br/images/logo.png"
                  fluid
                  alt="Responsive image"
                ></b-img>
              </div>

          <b-alert :variant="responseColor" :show="showAlert">{{
            responseMessage
          }}</b-alert>

          <div class="form-group">
            <input
              v-model="usuario.email" type="email"  required class="form-control-2 form-control" placeholder="Email" />
          </div>

          <div class="form-group">
            <input v-model="usuario.senha" :type="filedType"  required class="form-control-2 form-control"  placeholder="Password"  />
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
  background-color: #e42021;
  border:none;
  color:white !important;
  font-family:"WorkSansMedium";
  border-radius:100px;
}
.botao:hover{
  color:white;
  background-color: #fc8585;
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
html{
height: 100%;
}
h1{ 
  font-family: "WorkSansSemiBold";
  }
/*end geral*/
</style>
