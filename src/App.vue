<script >


export default {
  name: 'App',
  // data() {
  //   return {
  //     private: false
  //   }
  // },
  computed: {
    isVisible( pathName ) {
      const route = this.$router.options.routes.find(route => route.name === pathName );
      console.log(route.meta.login);
      return route.meta.login
    }
  }
}
 


</script>

<template>
  <nav>
    
  <RouterLink to="/">Home</RouterLink>
  <RouterLink to="/login">Login</RouterLink>
  <RouterLink to="/signup">SignUp</RouterLink>

 <RouterView > </RouterView>
  

  </nav>
</template>

<style >
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #164a42;
}

nav {
  padding: 50px;
}

nav a {
  font-weight: bold;
  color: #247bd2;
}

nav a.router-link-exact-active {
  color: #59327a;
}


</style>
