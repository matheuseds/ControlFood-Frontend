<template>
  <main class="background">
     <div class="container-naosei">
         <!--menu-->
      <div class="menu-bar">
        <div class="py-2">
          <!--content-->
          <nav class="mb-3">
            <b-nav vertical>
              <div style="text-align: center; margin: 4% 0px 17%">
                <b-img
                  class="img-menu"
                  src="https://designerelite.com.br/images/logo.png"
                  fluid
                  alt="Responsive image"
                ></b-img>
              </div>
              <NuxtLink to="/dashboardSite" class="nav-link"
                >Dashboard</NuxtLink
              >
              <NuxtLink to="/cadastrarEmpresa" class="nav-link menu-active"
                >Cadastrar Empresa</NuxtLink
              >
              <NuxtLink to="/cadastrarColaborador" class="nav-link"
                >Cadastrar Colaborador</NuxtLink
              >
              <NuxtLink to="/listarColaboradores" class="nav-link"
                >Listar Colaboradores</NuxtLink
              >
              <NuxtLink to="/listarEmpresas" class="nav-link  "
                >Listar Empresas</NuxtLink
              >
              <NuxtLink to="/relatorioGeral" class="nav-link"
                >Relatório Geral</NuxtLink
              > <button class="botaosair" @click="logout()">Sair</button>
            </b-nav>
          </nav>
          <!--end content-->
        </div>
      </div>
      <!--end menu-->
       <!--content -->
       <div class="container-content">
          <div class="col-md-12" style="width:80%; margin: 0 auto;">
                <h1 class="title-form">Cadastrar Empresa</h1>
               </div>
              <!--FORMULARIO-->
              <form @submit.prevent="cadastro">
                <b-alert :variant="responseColor" :show="showAlert">{{
                  responseMessage
                }}</b-alert>
                <div class="col-md-12">
                    <div class="form-group" style="width:25%;">
                    <input v-model="empresa.cnpj" class="form-control-2 form-control" type="text"  name="nome" id="cnpj" placeholder="CNPJ" v-maska="'##.###.###/####-##'" required/>
                  </div>
                </div>
                <!--linha 1-->
                <div class="col-md-12" style="display: flex;" >
                    <div class="form-group">
                      <input v-model="empresa.nomeEmpresa" class="form-control-2 form-control" type="text" placeholder="Nome da Empresa"  required  />
                    </div>
                    <div class="form-group">
                      <input v-model="empresa.email"  class="form-control-2 form-control" type="email" placeholder="E-mail" required />
                  </div>
                </div>

                <!--linha 2-->
                <div class="col-md-12" style="display: flex;" >
                    <div class="form-group">
                      <input  v-model="empresa.nomeResponsavel" class="form-control-2 form-control" type="text" placeholder="Nome do Responsável"  required  />
                    </div>
                    <div class="form-group">
                      <input v-model="empresa.contatoResponsavel" class="form-control-2 form-control" type="text" placeholder="Contato do Responsável" required />
                    </div>
                </div>

                <!--linha 3-->
                 <div class="col-md-12" style="display: flex;" >
                    <div class="col-md-6">
                     <div class="form-group" style="padding: 0;">
                          <input v-model="empresa.endereco" type="text" class="form-control-2 form-control"  placeholder="Rua Major Gote, n° 808" required  />
                      </div>
                    </div>
                    <div class="col-md-6" style="display: flex;" >
                        <div class="form-group" style="padding: 0;">
                          <input  v-model="empresa.cidade"  type="text" class="form-control-2 form-control"  style="width:97%;" placeholder="Patos de Minas"  required />
                        </div>
                       <div class="form-group" style="padding: 0;">
                          <input v-model="empresa.estado"  type="text" class="form-control-2 form-control" id="estado" placeholder="MG" v-maska="'AA'" required />
                        </div>
                    </div>
                  </div>
                <div class="form-group text-center">
                  <button type="submit" class="btn btn-red">Cadastrar</button>
                </div>
              </form>
               <!--end FORMULARIO-->
       </div>
       <!--end content -->
     </div>
  </main>
</template>

<script>
import { maska } from 'maska'

export default {
  directives: { maska },
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
      user_id: parseInt(localStorage.getItem('id')),
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
    logout() {
      localStorage.removeItem('token')
      localStorage.removeItem('id')
      this.$router.push({ name: 'index' })
    },
  },
}
</script>

<style>
* {
  font-family: sans-serif;
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
h1{ font-family: "WorkSansSemiBold";}
/*end geral*/
/*menu*/
.nav-link {
  color: #e42021;
  transition: 0.2s;
  padding: 5% 10%;
  font-family:"WorkSansRegular";
  font-size: 18px;
}
.nav-link:hover {
  color: #e42021;
  transition: 0.2s;
  background: #e42021;
  color: white;
}
.menu-active {
  background: #e42021;
  color: white !important;
}
.btn-secondary{
background-color:white;
color:#e42021;
border: none;
}
.btn-secondary:hover{
  color:rgb(214, 78, 78);
  background-color:white;
}
.btn-secondary:not(:disabled):not(.disabled):active, .btn-secondary:not(:disabled):not(.disabled).active, .show > .btn-secondary.dropdown-toggle {
    color: #e42021;
    background-color: white;
    border: none;
}
.btn-secondary:focus, .btn-secondary.focus{
     background-color: white;
     color:#343a40 !important;
    border: none;
    box-shadow: none;
}
.img-menu{
  width:70%;
}
/*end menu*/

/*cadastro empresa*/
.form-group {
width: 100%;
padding: 0 1%;
}
.btn-red{
   background-color:#e42021;
   padding: 10px 3%;
   border-radius: 100px;
   color: white;
   transition:0.2s;
   float: right;
   font-family: "WorkSansSemiBold";
   font-size: 18px;
   border:none;
}
.btn-red:hover{
  color: white;

  background-color: #fc8585;
  transition:0.2s;
}
.title-form{
      padding-left: 1.5%;
}
form{ 
    width: 80%;
    margin: 7% auto 0;
}
/*end cadastro empresa*/

</style>
