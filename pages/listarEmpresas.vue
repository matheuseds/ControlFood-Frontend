<template>
  <main class="background">
    <div class="container-naosei">
       <!--menu-->
    <div class="menu-bar">
        <div class="py-2">
          <!--content-->
          <nav class="mb-3">
            <b-nav vertical>
              <div style="text-align:center; margin: 4% 0px 17%;">
                  <b-img class="img-menu" src="https://designerelite.com.br/images/logo.png" fluid alt="Responsive image"></b-img>
              </div>
               <NuxtLink to="/dashboardSite" class="nav-link"
                >Dashboard</NuxtLink
              >
              <NuxtLink to="/cadastrarEmpresa" class="nav-link"
                >Cadastrar Empresa</NuxtLink
              >
              <NuxtLink to="/cadastrarColaborador" class="nav-link"
                >Cadastrar Colaborador</NuxtLink
              >
              <NuxtLink to="/listarColaboradores" class="nav-link"
                >Listar Colaboradores</NuxtLink
              >
              <NuxtLink to="/listarEmpresas" class="nav-link  menu-active"
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
    <!-- content -->
    <div class="container-content">
    <div class="container">
      <input type="search" id="form1" class="form-control" v-model="pesquisa"  placeholder="Pesquisar Empresas" />
      <b-alert :variant="responseColor" :show="showAlert">{{
        responseMessage
      }}</b-alert>
      <table class="content-table table">
        <thead class="table-title">
           <h1>Empresas</h1>
        </thead>
        <div>
          <!--MODAL EXCLUIR--> 
          <b-modal id="modal-1" title="Excluir empresa" ok-title="Sim"  cancel-title="Não" @ok="excluirEmpresa()" >
            <p class="my-4">Você deseja excluir esta empresa?</p>
          </b-modal>
        </div>
       <!--FIM MODAL EXCLUIR-->
       <!--MODAL EDIT-->
        <b-modal id="modal-editarempresa" title="Editar Empresa" ok-title="Confirmar"  cancel-title="Cancelar" @ok="editarEmpresa()" >
          <div >
            <label for="number">Nome da empresa:</label>
            <input  v-model="empresa.nomeEmpresa"    type="text" placeholder="Nome da Empresa" required />
          </div>
          <div >
            <label for="email">E-mail:</label>
            <input v-model="empresa.email"  type="email" placeholder="E-mail" required />

            <div >
              <label for="email">Nome do responsável:</label>
              <input v-model="empresa.nomeResponsavel"   type="text" placeholder="Nome da Empresa"  required  />
            </div>

            <div >
              <label for="email">Contato do responsável:</label>
              <input v-model="empresa.contatoResponsavel"   type="text" placeholder="Contato do Responsável"  required />
            </div>

            <div >
              <label for="email">Endereço:</label>
              <input  v-model="empresa.endereco"  type="text" placeholder="Endereço da Empresa"  required />
            </div>

            <div >
              <label for="email">Cidade:</label>
              <input  v-model="empresa.cidade"   type="text" placeholder="Cidade"  required />
            </div>

            <div>
              <label for="email">Estado:</label>
              <input  v-model="empresa.estado"    type="text" placeholder="Estado"  required />
            </div>
          </div>
        </b-modal>
          <!--FIM MODAL EDIT-->
        <!--container lista-->
        <div class="table-container">
           <tbody v-for="empresa in empresasFiltradas" :key="empresa.id">
            <div class="table-row">
              <div class="table-id">
                <h1>{{ empresa.id }}</h1>
              </div>
               <div class="table-user">
                    <h1>{{ empresa.nomeEmpresa }}</h1>
                    <div class="table-user-description">
                        <p style="margin-right:2%;">{{ empresa.contatoResponsavel }}</p>
                        <p>{{ empresa.email }}</p>
                    </div>
                </div>
                 <div class="table-btn">
                    <b-button id="btn-edit" class="btn-modal" v-b-modal.modal-editarempresa
                        @click="abrirModaldeEdicao(empresa)"
                      >
                        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="currentColor" class="bi bi-pen" viewBox="0 0 16 16">
                                <path d="m13.498.795.149-.149a1.207 1.207 0 1 1 1.707 1.708l-.149.148a1.5 1.5 0 0 1-.059 2.059L4.854 14.854a.5.5 0 0 1-.233.131l-4 1a.5.5 0 0 1-.606-.606l1-4a.5.5 0 0 1 .131-.232l9.642-9.642a.5.5 0 0 0-.642.056L6.854 4.854a.5.5 0 1 1-.708-.708L9.44.854A1.5 1.5 0 0 1 11.5.796a1.5 1.5 0 0 1 1.998-.001zm-.644.766a.5.5 0 0 0-.707 0L1.95 11.756l-.764 3.057 3.057-.764L14.44 3.854a.5.5 0 0 0 0-.708l-1.585-1.585z"/>
                              </svg>
                      </b-button>

                      <b-button class="btn-modal"  v-b-modal.modal-1 @click=" id = empresa.id" >
                        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="currentColor" class="bi bi-trash3" viewBox="0 0 16 16">
                                <path d="M6.5 1h3a.5.5 0 0 1 .5.5v1H6v-1a.5.5 0 0 1 .5-.5ZM11 2.5v-1A1.5 1.5 0 0 0 9.5 0h-3A1.5 1.5 0 0 0 5 1.5v1H2.506a.58.58 0 0 0-.01 0H1.5a.5.5 0 0 0 0 1h.538l.853 10.66A2 2 0 0 0 4.885 16h6.23a2 2 0 0 0 1.994-1.84l.853-10.66h.538a.5.5 0 0 0 0-1h-.995a.59.59 0 0 0-.01 0H11Zm1.958 1-.846 10.58a1 1 0 0 1-.997.92h-6.23a1 1 0 0 1-.997-.92L3.042 3.5h9.916Zm-7.487 1a.5.5 0 0 1 .528.47l.5 8.5a.5.5 0 0 1-.998.06L5 5.03a.5.5 0 0 1 .47-.53Zm5.058 0a.5.5 0 0 1 .47.53l-.5 8.5a.5.5 0 1 1-.998-.06l.5-8.5a.5.5 0 0 1 .528-.47ZM8 4.5a.5.5 0 0 1 .5.5v8.5a.5.5 0 0 1-1 0V5a.5.5 0 0 1 .5-.5Z"/>
                              </svg>
                      </b-button>
                 </div>
            </div>
            </tbody>
        </div>
       <!--end container lista-->
      </table>
    </div>
    </div>
    <!-- end content-->
    </div>
  </main>
</template>

<script >
export default {
  data: () => ({
    empresa: {
      nomeEmpresa: '',
      nomeResponsavel: '',
      email: '',
      contatoResponsavel: '',
      endereco: '',
      cidade: '',
      estado: '',
      id: '',
    },

    empresas: [],
    pesquisa: '',
    id: null,

    responseColor: null,
    responseMessage: null,
    showAlert: false,
  }),
  async fetch() {
    this.empresas = await this.$axios.$get('/empresa')
  },
  computed: {
    empresasFiltradas() {
      return this.empresas.filter((empresa) =>
        empresa.nomeEmpresa.toLowerCase().includes(this.pesquisa.toLowerCase())
      )
    },
  },
  methods: {
    async excluirEmpresa() {
      await this.$axios.$delete(`/empresa/${this.id}`)
      const filterEmpresas = this.empresas.filter(
        (empresa) => empresa.id !== this.id
      )

      this.empresas = filterEmpresas
    },

    async editarEmpresa() {
      await this.$axios.$put(`/empresa/${this.empresa.id}`, this.empresa)
      this.$fetch()
    },

    abrirModaldeEdicao(empresa) {
      this.empresa = Object.assign({}, empresa)
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
.content-table {
  width: 100%;
  margin: 0 auto !important;
  }
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
/*cadastro input*/
.form-control {
  color: #333030;
  background-color: #fff;
  border-bottom: 1px solid #333030 !important;
  border: 0px solid;
  border-radius: 0;
  margin: 10px 0px;
  font-family: "WorkSansRegular";
  font-size: 20px;
  display: block;
  width: 35%;
  float: right;
}
.form-control:focus{
  background: #e2e2e2;
   border: none !important;
}
.form-group {
width: 100%;
padding: 0 1%;
}
/*end input*/
</style>

