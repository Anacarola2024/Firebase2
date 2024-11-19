<template>
    
<div>
<h1>Registro</h1>
<input type="text" placeholder="email" v-model="email">
<input type="password" placeholder="password" v-model="password">
<button @click="register">Registrar</button>
  </div>

</template>

<script>
import firebaseAuthPlugin from '../../auth';
import app from '../../firebaseConfig';

export default {
    name: 'SingUpView',
    data(){
        return{
            email: '',
            password: ''
        }
    },
    methods: {
        async register(){
            const {email, password} = this;
            if ([email, password].includes('')) {
                return alert('Todos los campos son obligatorios');
            }
            try {
                const firebaseAuth = firebaseAuthPlugin(app)
                const userCredential = await firebaseAuth.createUser (firebaseAuth.auth, email, password);
                alert('Registro completado con exito!')
                this.email = ''
                this.password = ''

                const user = userCredential.user;
                 console.log({user});
                
            } catch (error) {

                
    if (error.code === 'auth/email-already-in-use') {
        alert('Este correo ya está registrado.');
    } else if (error.code === 'auth/invalid-email') {
        alert('Correo no válido. Por favor, verifica el formato.');
    } else if (error.code === 'auth/weak-password') {
        alert('La contraseña es demasiado débil. Usa al menos 6 caracteres.');
    } else {
        alert('Error al registrar el usuario: ' + error.message);
    }
    console.error('Error al crear el usuario:', error);
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