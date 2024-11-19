<template>
<div>
<h1>Inicio de Sesion</h1>
<input type="text" placeholder="email" v-model="email">
<input type="password" placeholder="password" v-model="password">
<button @click="signIn">Iniciar Sesion</button>
  </div>
  
</template>

<script>
import firebaseAuthPlugin from '../../auth';
import app from '../../firebaseConfig';

export default {
    name: 'LoginView',
    data(){
        return{
            email: '',
            password: ''
        }
    },
    methods: {
        async signIn(){
            const {email, password} = this;
            if ([email, password].includes('')) {
                return alert('Todos los campos son obligatorios');
                try {
                    const firebaseAuth = firebaseAuthPlugin(app)
                    const {user} = await firebaseAuth.loginUser (firebaseAuth.auth, email, password);
                    console.log(user);


                    this.$router.options.routes.forEach(route => {
                        if (route.name === 'Home') {
                            route.meta.login = false
                            return
                        }
                        route.meta.login = true

                    });
                    this.$router.push('/')
                } catch (error) {
                    console.error('error al crear el usuario', error);
                    alert('Credenciales Invalidas')
                    this.email = ''
                    this.password = ''
                }
            }
        }
    }
}

</script>

<style scoped>
  .wrapper {
        max-width: 120rem;
        width: 90%;
        margin: 0 auto;
       
    }

    form {
        display: flex;
        flex-direction: column;
        gap: 1rem;
    }
</style>