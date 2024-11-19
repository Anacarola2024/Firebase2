
<script>
import firebaseAuthPlugin from '../../auth';
export default {
  data() {
    return {
      email: '',
      password: ''
    }
  },
  methods: {
    async signIn () {
      try {
      const {email, password} = this

    
      const {user} = await signInWithEmailAndPassword(auth, email, password)
      
      alert ('usuario logeado')
      console.log( 'usuario logeado',user)
       
      } catch (error) {
        console.error('error al iniciar sesion',error)
      }
    }
  }
}

</script>

<template>
 
  <div>
<h1>Inicio de Sesion</h1>
<input type="text" placeholder="email" v-model="email">
<input type="password" placeholder="password" v-model="password">
<button @click="signIn">Iniciar Sesion</button>
  </div>
  

</template>