<template>
    <main class="form-signin main">
        <div class="card ">
               <div class="card-body mt-n1">
                    <form @submit.prevent="login">
                        <h2 class="h3 mb-3 fw-normal text-center">Faça o Login</h2>

                        <div class="form-group">
                            <label>Email</label>
                            <input type="email" required class="form-control form-control-lg" placeholder="Email" />
                            
                        </div>

                        <div class="form-group">
                            <label>Senha</label>
                            <input type="password" required class="form-control form-control-lg" placeholder="Password"/>
                            
                        </div>

                        <b-button class="w-100 btn btn-lg btn-primary botao" type="submit">Entrar</b-button>

                        <b-checkbox class="senha">Esqueci minha senha</b-checkbox>

                    </form>

                </div>
        </div>
    </main>
    
</template>

<script>
export default{
    data: () => ({
        email: '',
        password: '',
    }),

    methods: {
        login(){
            alert('login')
        }
    }
}
</script>

<style>
   .main{
       width: 100vw;
   }
    .botao{
        width: 6.0rem !important;
        min-width: 320px !important;
        max-width: 800px !important;
        margin-top: 2% !important;
        
    }
    .mt-n1 {
        margin-left: auto !important;
        margin-right: auto !important;
        min-width: 320px !important;
        max-width: 800px !important;
        justify-content: center !important;
        align-items: center !important;
        margin-top: 15% !important;
        margin-bottom: 15% !important;
    }
    .senha{
        margin-top: 7% !important;
    }
    

</style>