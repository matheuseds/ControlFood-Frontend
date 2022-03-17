<template>
    <main class="form-signin">
        <div class="card">
               <div class="card-body mt-n1">
                    <form>
                        <h2 class="h3 mb-3 fw-normal text-center">Faça o Login</h2>

                        <div class="form-group">
                            <label>Email</label>
                            <input type="email" class="form-control form-control-lg" placeholder="Email" />
                            
                        </div>

                        <div class="form-group">
                            <label>Senha</label>
                            <input type="password" class="form-control form-control-lg" placeholder="Password"/>
                            
                        </div>

                        <router-link class="w-100 btn btn-lg btn-primary botao" type="submit" to="/signup">Entrar</router-link>

                    </form>

                </div>
        </div>
        <p class="mt-3 mb-3 text-muted text-center">© 2022</p>
    </main>
    
</template>

<script>
export default{
    data: () => ({
        email: '',
        password: '',
    }),
}
</script>

<style>
   

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

</style>