<template>
  <main class="background">
    <!--menu-->
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
              <NuxtLink to="/cadastrarEmpresa" class="nav-link"
                >Cadastrar Empresa</NuxtLink
              >
              <NuxtLink to="/cadastrarColaborador" class="nav-link menu-active"
                >Cadastrar Colaborador</NuxtLink
              >
              <NuxtLink to="/listarColaboradores" class="nav-link"
                >Listar Colaboradores</NuxtLink
              >
              <NuxtLink to="/listarEmpresas" class="nav-link"
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
       <!--content-->
       <div class="container-content">
           <div class="col-md-12">
             <div class="col-md-12" style="width:80%; margin: 0 auto;">
                <h1 class="title-form">Cadastrar Colaboradores</h1>
               </div>
              <form @submit.prevent="cadastro">
                <b-alert :variant="responseColor" :show="showAlert">{{
                  responseMessage
                }}</b-alert>
                 <!--linha 1-->
                <div class="col-md-12" style="display: flex;" >
                      <div class="form-group">
                    <input v-model="colaborador.nome" class="form-control-2 form-control" type="text" placeholder="Nome" required/>
                  </div>
                  <div class="form-group">
                    <input v-model="colaborador.cpf" class="form-control-2 form-control" type="text" placeholder="CPF" v-maska="'###.###.###-##'" required/>
                  </div>
                  </div>
                <!--linha 2-->
                <div class="col-md-12" style="display: flex;" > 
                  <div class="form-group">
                    <input v-model="colaborador.nome_empresa" class="form-control-2 form-control" type="text" placeholder="Nome da Empresa" required/>
                  </div>
                  <div class="form-group">
                    <input v-model="colaborador.email" class="form-control-2 form-control" type="email" placeholder="E-mail" required/>
                  </div>
                </div>
                 <div class="form-group text-center">
                  <button type="submit" class="btn btn-red">Cadastrar</button>
                </div>
              </form>
    </div>
       </div>
        <!--end content-->
    </div>
  </main>
</template>

<script>
import { maska } from 'maska'

export default {
  directives: { maska },

  data: () => ({
    colaborador: {
      nome: '',
      cpf: '',
      nome_empresa: '',
      email: '',
      user_id: localStorage.getItem('token'),
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
      console.log(this.colaborador.cpf)
      const response = await this.$axios.$post('/colaborador', this.colaborador)
      try {
        if (response.status === 203) {
          this.responseColor = 'danger'
        } else {
          this.responseColor = 'success'
        }

        this.responseMessage = response.message
        this.showAlert = true
      } catch (error) {
        console.log(error)
        this.responseColor = 'danger'
        this.responseMessage = response.message
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
.container-naosei{
  width:100%;
  display:flex;
}
.container-content{
  width:80%;
  padding-top: 3%;
}
/*end geral*/
/*menu*/
.menu-bar{
  width:20%;
  height:100%;
}
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
.img-menu{
  width:70%;
}
/*end menu*/
/*table*/
.table-row{
  width:100%;
  display:flex;
   align-items: center;
   padding: 20px 3%;
}
.table-container{
  overflow-y:scroll;
  height: 650px;
  display: flex;
  flex-direction: column;
}
.table-id{
  width: 10%;
  color:#333030;
}
.table-id h1{
  font-size: 25px;
}
.table-title{
  background-color:#e42021;
}
.table-title h1{
  font-size: 35px;
  color:white;
  margin: 10px 0px 10px 3%;
}
.table-user{
 width: 60%;
 color:#333030;
}
.table-user h1{
   font-size: 25px;
   font-family:"WorkSansSemiBold";
   margin: 0;
}
.table-user p{
  font-size: 15px;
  font-family:"WorkSansRegular";
   margin: 0;
}
.table-user-description{
  display:flex;
}
.table-btn{
  width:40%;
  text-align: right;
}
.btn-modal{
  color:#333030;
}
#btn-edit:hover{
  color:#0082be !important;
  transition: 0.2s;
}
.btn-secondary:focus, .btn-secondary.focus{
     background-color: white;
     color:#333030 !important;
    border: none;
    box-shadow: none;
}
/*end table*/  
/*cadastro empresa*/
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